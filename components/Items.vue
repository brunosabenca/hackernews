<template>
    <div class="code">
        <ul class="list pa2">
          <li class="item" v-for="item in items" :key="item.id">
            <div class="score">
              {{item.score}}
            </div>
            <div class="title">
              {{item.title}}
              <template v-if="item.url">
                  <a :href="item.url">{{item.url | hostname}}</a>
              </template>
            </div>
            <div class="details">
              by <nuxt-link :to="'/user/' + item.by">{{item.by}}</nuxt-link>
              {{item.time | timeSince}} ago
            </div>
            <template v-if="item.descendants">
                <div class="comments">
                  <nuxt-link :to="'/item/' + item.id">
                    {{item.descendants}} comments
                  </nuxt-link>
                </div>
            </template>
          </li>
        </ul>
    </div>
</template>

<script>
import { mapState } from 'vuex'

export default {
  computed: mapState([
    'ids',
    'items'
  ])
}
</script>

<style scoped>
.item {
  display: grid;
  grid: repeat(4, 1.5em) / repeat(10, 1fr);
  grid-row-gap: 1em;
}

.score{
  grid-row: 1 / -1;
  grid-column: span 1;
  align-self: center;
  justify-self: center;
}

.title{
  grid-row: 1 / 3;
  grid-column: 2 / -2;
  align-self: end;
}

.details {
  grid-row: 3 / -1;
  grid-column: 6 / -2;
}

.comments {
  grid-row: 3 / -1;
  grid-column: 2 / 6;
}

.details {
  grid-row: 3 / -1;
  grid-column: 6 / -2;
}
</style>
