<template>
  <view class="index">
    <view class="text">{{ JSON.stringify(student) }}</view>
    <at-button size="small" @click="handleShowToast" type="primary"
      >按钮文案</at-button
    >
    <at-toast
      :onClose="handleClose"
      :isOpened="showToast"
      :text="text"
      :icon="icon"
    ></at-toast>
  </view>
</template>

<script lang="ts">
import { AtButton, AtToast } from "taro-ui-vue3";
import { defineComponent, reactive, toRefs, computed, watch } from "vue";
import "./index.scss";

interface Student {
  name: string;
  age: number;
  sex: string;
}

export default defineComponent({
  components: {
    AtButton,
    AtToast,
  },

  setup() {
    const student: Student = {
      name: "dexter",
      age: 18,
      sex: "男",
    };

    const state = reactive({
      icon: "eye",
      showToast: false,
      student,
    });

    watch(
      () => state.student,
      () => {
        console.log(state.student);
      },
      { deep: true }
    );

    const text = computed((): string => {
      return String(Math.random());
    });

    const handleShowToast = (): void => {
      state.student.name = "hello";
      state.showToast = true;
    };

    const handleClose = (): void => {
      state.showToast = false;
    };

    return {
      ...toRefs(state),
      student,
      handleShowToast,
      handleClose,
      text,
    };
  },
});
</script>
