<template>
<div class="player">
  <v-container fluid grid-list-xs text-xs-center>
    <v-layout row wrap justify-start>
      <v-flex xs12 ma-1 pa-0>
        <span>Public area</span>
      </v-flex>
    </v-layout>
    <v-layout row nowrap justify-start>
      <v-flex xs2 ma-1 pa-0>
      <draggable element="div" :list="arena" class="material" :move="beforeMove" @end="onEnd" :options="{group:'cards'}">
        <div v-for="(card, index) in arena" :key="index">
          <span v-if="card.suit=='label'">
            [Dragging Card Space]
          </span>
          <div v-else class="card">
            {{card.suit}} {{card.number}}
          </div>
        </div>
      </draggable>
      </v-flex>
    </v-layout>
  </v-container>
    <br />
  <v-container fluid grid-list-xl>
    <v-layout row wrap justify-start>
      <v-flex xs3 ma-1 pa-0>
      <span>Private area</span>
      <draggable :list="hand" class="material" :move="beforeMove" @end="onEnd" :options="{group:'cards'}" element="div">
        <div v-for="(card, index) in hand" :key="index">
          <span v-if="card.suit=='label'">
            [Dragging Card Space]
          </span>
          <div v-else class="card">
            {{card.suit}} {{card.number}}
          </div>
        </div>
      </draggable>

      </v-flex>
    </v-layout>
  </v-container>
    <div class="flex" v-show="showButtons">
      <v-btn @click="hit">Hit</v-btn>
      <v-btn @click="stand">Stand</v-btn>
    </div>

</div>
</template>

<script>
import draggable from "vuedraggable";

import pick from '../utils/deck'
import calc from '../utils/calc'
import Card from './Card'

export default {
  name: 'player',
  components: { draggable, Card },
  props: ['showButtons'],
  data () {
    return {
      hand: [ { suit: "label"} ],
      arena: [{ suit: "label"}],
      result: 0,
    }
  },
  created: function () {
    this.hand.push(pick());
    this.hand.push(pick());
    this.hand.push(pick());
    this.hand.push(pick());
    this.arena.push(pick());
    this.arena.push(pick());
    this.arena.push(pick());
    this.result = calc(this.hand);
  },
  methods: {
    hit () {
      this.hand.push(pick());
      this.result = calc(this.hand);
    },
    stand () {
      this.$emit('stand', this.result)
    },
    beforeMove: function(evt) {
      return evt.draggedContext.element.name !== 'Drag Area';
    },
    onEnd: function(evt) {
      console.log(evt);
    },
  },
  watch: {
    result: function (newValue, oldValue) {
      if (newValue === 'Bust') {
        this.$emit('stand', newValue)
      }
    }
  }
}
</script>