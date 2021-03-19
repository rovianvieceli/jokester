<template>
  <div id="jokester">
    <div class="row">
      <div class="col-md-12">
        <h3>Got Jokes?</h3>
        <button class="btn btn-primary" @click="initJokes">
          Add Ten Randon Jokes
        </button>
        <button class="btn btn-primary" @click="addJoke">Add a Joke</button>
      </div>
      <div class="col-md-12">
        <div
          v-for="(type, index) in types"
          :key="index"
          class="form-check form-switch form-check-inline"
        >
          <input
            :id="`joke-${type}`"
            type="checkbox"
            :value="type"
            v-model="checkdTypes"
            checked
            class="form-check-input"
          />
          <label class="form-check-label" :for="`joke-${type}`"
            >{{ type }}
          </label>
        </div>
      </div>

      <Joke
        v-for="(joke, key, index) in $store.state.jokes"
        v-show="checkdTypes.includes(joke.type)"
        :joke="joke"
        :index="index"
        :key="key"
      />
    </div>
  </div>
</template>

<script>
import { mapActions } from "vuex";
import Joke from "./Joke.vue";

export default {
  data() {
    return {
      types: ["general", "knock-knock", "programming"],
      checkdTypes: ["general", "knock-knock", "programming"],
    };
  },
  methods: mapActions(["initJokes", "addJoke"]),
  components: {
    Joke,
  },
};
</script>
