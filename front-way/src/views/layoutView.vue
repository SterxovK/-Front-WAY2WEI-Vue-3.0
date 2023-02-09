<template>
  <SectionInfo></SectionInfo>
  <SectionCheckbox></SectionCheckbox>
</template>

<script>
// @ is an alias to /src
import SectionInfo from '@/components/SectionInfo.vue'
import SectionCheckbox from '@/components/SectionCheckbox.vue'

export default {
  name: 'layoutView',
  components: {
    SectionInfo,
    SectionCheckbox
  }
}
</script>
