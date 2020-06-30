<template>
  <div class="w-full">
    <textarea 
      class="w-full mb-6 border-2 border-gray-400 rounded"
      v-model="step.body"
    >
    </textarea>
    <div class="bg-white p-8 rounded-lg text-gray-600 ">
      <step-show
        :currentStep="step.body"
      />
    </div>
    
  </div>
</template>

<script type="text/javascript">
 
  import StepShow from '@/components/snippets/StepShow'
  export default {
    props: {
      step: {
        required: true,
        type: Object
      }
    },
    data () {
      return {
        formula: '$$x = {-b \\pm \\sqrt{b^2-4ac} \\over 2a}.$$'
      }
    },
    components: {
      StepShow,
    },
    mounted () {
      console.log(this.step)
    }
  }
</script>