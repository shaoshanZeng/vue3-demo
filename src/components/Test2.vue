
<script>
import { reactive, ref, toRef, toRefs } from "vue";
function useFeatureX() {
  const state1 = reactive({
    foo1: 1,
    bar1: 2,
  });
  return toRefs(state1);
}

export default {
  props: {
    title: String,
  },
  setup(props) {
    console.log(props.title); // 如果结构了props，解构出来的变量就会失去响应式，为解决此问题就出现了toRef和toRefs

    const count = ref(0);
    const state = reactive({
      foo: 1,
      bar: 2,
    });

    // 将对象/props中的某个property转为一个ref
    const fooRef = toRef(state, "foo"); // 不同于const fooRef = ref(state.foo);因为ref接收到的是个纯数值
    fooRef.value++;
    console.log("foo:" + state.foo);

    //将对象/props转化为一个全是ref的对象，然后解构
    const { bar } = toRefs(state);
    console.log("bar:" + bar.value);
    const newState = toRefs(state);
    newState.foo++;
    console.log("newFoo:" + newState.foo.value);

    // 第三种 头部定义个方法先转toRefs，再在此处解构
    const { foo1, bar1 } = useFeatureX();

    return {
      count,
      foo1,
      bar1,
    };
  },
  mounted() {
    console.log("count:" + this.count); // 0
  },
};
</script>
<template>
  <div>
    <button @click="count++">{{ count }}</button>
    {{ foo1 }}
    {{ bar1 }}
  </div>
</template>
