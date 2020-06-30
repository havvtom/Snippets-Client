<template>
  <ais-instant-search-ssr>
    <div class="mb-16 bg-white">
      <div class="container py-10 pb-16">
        <div class="flex justify-between items-center mb-6">
          <h1 class="text-4xl text-gray-700 font-medium leading-tight mb-4">
            Search
          </h1>
          <client-only>
            <ais-powered-by/>
          </client-only>
        </div>
        <ais-search-box
          placeholder="Search Snippets"
          :class-names="{
            'ais-SearchBox': 'w-full',
            'ais-SearchBox-input': 'w-full border-2 border-gray-400 rounded-lg block p-4 text-lg',
            'ais-SearchBox-submit': 'hidden',
            'ais-SearchBox-submitIcon': 'hidden',
            'ais-SearchBox-reset': 'hidden',
          }"
        /> 
      </div>      
    </div>
    <div class="container">
      <ais-state-results>
        <div slot-scope="{ query }">
          <template v-if="query.length">
            <ais-stats>
              <h1 
                class="text-xl font-medium text-gray-600 mb-6"
                slot-scope="{ nbHits }"
              >
                Snippets {{ nbHits }}
              </h1>  
            </ais-stats> 

            <ais-hits>
              <div slot="item" slot-scope="{ item }">
                <search-snippet-card
                  :snippet="item"
                />
              </div>
            </ais-hits> 
          </template>
        </div>
      </ais-state-results>      
    </div>
  </ais-instant-search-ssr>
</template>

<script>
import SearchSnippetCard from './components/SearchSnippetCard'
import {
  AisInstantSearchSsr,
  AisIndex,
  AisConfigure,
  AisRefinementList,
  AisHits,
  AisHighlight,
  AisSearchBox,
  AisStats,
  AisStateResults,
  AisPagination,
  createServerRootMixin,
  AisPoweredBy,
} from 'vue-instantsearch'; // eslint-disable-line import/no-unresolved
import algoliasearch from 'algoliasearch/lite';

const searchClient = algoliasearch(
  '3LEB06DEL9',
  'YzhmMTY0MGUzODQ2MDc4Y2Q0NTg0ZDZkY2EzMGEwNDU2ODJmMThlYTgzNjMzMWNmZmM1NjQwNDEyZTMyOWI3N2ZpbHRlcnM9aXNfcHVibGljJTNBdHJ1ZQ=='
);

export default {
  data () {
    return {
      results: null
    }
  },
  mixins: [
    createServerRootMixin({
      searchClient,
      indexName: 'snippets',
    }),
  ],
  serverPrefetch() {
    return this.instantsearch.findResultsState(this).then(algoliaState => {
      this.$ssrContext.nuxt.algoliaState = algoliaState;
    });
  },
  beforeMount() {
    this.results = window.__NUXT__.algoliaState;

    this.instantsearch.hydrate(this.results);
  },
  components: {
    AisInstantSearchSsr,
    AisIndex,
    AisConfigure,
    AisRefinementList,
    AisHits,
    AisHighlight,
    AisSearchBox,
    AisStats,
    AisStateResults,
    AisPagination,
    SearchSnippetCard,
    AisPoweredBy
  },
  mounted () {
   
  },
  head() {
    return {
      title: 'Search'
    }
  }
};
</script>

