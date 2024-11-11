<script scope>
export default {
  data() {
    return {
      count: 0,
      name: "irsan",
    };
  },
  methods: {
    increase() {
      this.count++;
    },
    decrease() {
      this.count--;
    },

    ganteng(name) {
      if (this.count > 0) {
        this.name = name;
      }
    },
  },
};
</script>

<template>
  <div class="flex justify-center items-center min-w-[400px] min-h-[500px]">
    <div class="flex-col justify-center gap-11 items-center bg-slate-300 p-5">
      <div class="text-bold text-4xl font-semibold text-center mx-auto">Count</div>
      <div id="value" class="count font-bold text-6xl text-center">{{ count }} {{ name }}</div>
      <div class="flex justify-center items-center gap-3 my-5 h-full">
        <button @click="increase" id="increase" class="px-8 py-2 text-white text-2xl bg-slate-500">+</button>
        <button @click="decrease" id="decrease" class="px-8 py-2 text-white text-2xl bg-slate-500">-</button>
        <button @click="ganteng('iya')" id="decrease" class="px-8 py-2 text-white text-2xl bg-slate-500">Change</button>
      </div>
    </div>
  </div>
</template>
