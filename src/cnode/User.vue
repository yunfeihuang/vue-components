<template>
  <page>
    <x-nav slot="header" title="用户详情"></x-nav>
    <page-body slot="body" :class="clas">
      <div v-if="slideIn">
        <div>
          <div class="userinfo">
            <x-img lazyload :src="user.avatar_url" class="user-avatar" />
            <h4>{{user.loginname}}</h4>
            积分：{{user.score}}
          </div>
          <divider></divider>
          <div class="user-title">最近创建的话题</div>
          <div class="user-comments">
            <divider></divider>
            <base-item v-for="item in user.recent_topics" :key="item.id+'topics'">
              <router-link slot="img" :to="item.user_href">
                <x-img :src="item.author.avatar_url"/>
              </router-link>
              <router-link slot="content" :to="item.href">
                <h4>{{item.title}}</h4>
                <div class="assist">
                {{item.last_reply_at}}
                </div>
              </router-link>
            </base-item>
          </div>
          <div class="user-title">最近参与的话题</div>
          <div class="user-comments">
            <divider></divider>
            <list-item divider
              v-for="item in user.recent_replies"
              :key="item.id+'replies'"
              :image="item.author.avatar_url"
              image-style="width:1rem">
              <div>
                <h4 style="margin:0">{{item.title}}</h4>
                <div class="assist">
                {{item.last_reply_at}}
                </div>
              </div>
            </list-item>
          </div>
        </div>
      </div>
    </page-body>
  </page>
</template>

<script>
import { mapState } from 'vuex'

export default {
  computed: {
    ...mapState({
      user: state => state.cnode.user
    }),
    clas () {
      return ['user', {
        'topic-placeholder': Object.keys(this.user).length === 0 || !this.slideIn
      }]
    }
  },
  created () {
    this.$store.dispatch('cnode/user', {
      id: this.$route.params.id
    })
  },
  beforeRouteUpdate (to, from, next) {
    this.$store.dispatch('cnode/user', {
      id: to.params.id
    })
    next()
  }
}
</script>

<style lang="scss">
  .user{
    &-placeholder{
      background:url('./images/body_placeholder.png') no-repeat;
      background-size:100% auto;
      >div{
        opacity:0
      }
    }
  }
  .userinfo{
    text-align:center;
    background:#fff;
    padding:0.2rem 0;
    h4{
      font-size:1.1em;
    }
  }
  .user-avatar{
    width:1rem;
    height:1rem;
    margin: auto;
  }
  .user-comments{
    background:#fff;
  }
  .user-title{
    margin:15px 5px 5px 5px;
  }
</style>
