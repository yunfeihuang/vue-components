<template>
  <page>
    <x-nav slot="header" title="Badge"></x-nav>
    <page-body slot="body">
      <group>
        <cell>
          <div slot="title">红点</div>
          <div slot="value">新消息<badge class="badge"/></div>
        </cell>
        <cell>
          <div slot="title" @click="handleClick">个位数红点(点击累加)</div>
          <div slot="value" @click="handleClick">新消息 <badge class="badge" :text="count"/></div>
        </cell>
        <cell>
          <div slot="title">超出最大值显示(ellipsis)红点</div>
          <div slot="value">新消息 <badge class="badge" :text="Number(20)"/></div>
        </cell>
        <cell>
          <div slot="title">多位数红点</div>
          <div slot="value">新消息 <badge class="badge" text="888"/></div>
        </cell>
      </group>
    </page-body>
  </page>
</template>

<script>
export default {
  methods: {
    handleClick () {
      this.count++
    }
  },
  data () {
    return {
      count: 8
    }
  }
}
</script>

<style lang="scss">

</style>
