<template>
  <span v-html="stuff"></span>
</template>

<script>
export default {
  name: 'MultiColorText',
  props: ['text'],
  computed: {
    stuff: function () {
      return colorText(this.text)
    }
  }
}

const colors = ['#b33422', '#58a623', '#686b97']

function colorText(text = '') {
  let i = 0

  return text.split('').reduce((prev, cur) => {
    if (cur !== ' ') {
      i = colors[i] ? i : 0
      cur = `<span style='color: ${colors[i]}'>${cur}</span>`
      i++
    }

    return [...prev, cur]
  }, []).join('')
}
</script>
