<template>
  <div class="phone">
    <FormGenerator v-bind="{ ...formAttrs }" />
  </div>
  <JsonViewer :value="formAttrs.model" expand previewMode />
</template>

<script lang="tsx" setup>
import type { FormAttrs } from 'vant3-generator/lib/type'
import { FormGenerator } from 'vant3-generator'
import { Toast } from 'vant'
import { ref } from 'vue'

const formAttrs = ref<FormAttrs>({
  model: {},
  formOption: [
    {
      type: 'stepper',
      formItem: {
        name: 'key1',
        label: '基础用法',
      },
    },
    {
      type: 'stepper',
      formItem: {
        name: 'key2',
        label: '步长设置',
      },
      control: {
        step: 2
      }
    },
    {
      type: 'stepper',
      formItem: {
        name: 'key3',
        label: '限制输入范围',
      },
      control: {
        min: 2,
        max: 8
      }
    },
    {
      type: 'stepper',
      formItem: {
        name: 'key4',
        label: '限制输入整数',
      },
      control: {
        integer: true
      }
    },
    {
      type: 'stepper',
      formItem: {
        name: 'key5',
        label: '禁用状态',
      },
      control: {
        disabled: true
      }
    },
    {
      type: 'stepper',
      formItem: {
        name: 'key6',
        label: '禁用输入框',
      },
      control: {
        disableInput: true
      }
    },
    {
      type: 'stepper',
      formItem: {
        name: 'key7',
        label: '固定小数位数',
      },
      control: {
        step: 0.2,
        decimalLength: 1,
      }
    },
    {
      type: 'stepper',
      formItem: {
        name: 'key8',
        label: '自定义大小',
      },
      control: {
        inputWidth: '40px',
        buttonSize: '32px'
      }
    },
    {
      type: 'stepper',
      formItem: {
        name: 'key9',
        label: '异步变更',
      },
      control: {
        beforeChange: (value: string) => {
          Toast.loading({ forbidClick: true });
          return new Promise((resolve) => {
            setTimeout(() => {
              Toast.clear();
              // 在 resolve 函数中返回 true 或 false
              resolve(true);
            }, 500);
          });
        }
      }
    },
    {
      type: 'stepper',
      formItem: {
        name: 'key10',
        label: '圆角风格',
      },
      control: {
        disableInput: true,
        buttonSize: 22,
        theme: 'round'
      }
    },
    {
      type: 'stepper',
      formItem: {
        name: 'key11',
        label: '监听',
      },
      control: {
        onChange: (value: string, detail: { name: string }) => { console.log(`onChange:${value} ${JSON.stringify(detail)}`) },
        onOverlimit: () => { console.log(`onOverlimit`) },
        onPlus: () => { console.log(`onPlus`) },
        onMinus: () => { console.log(`onMinus`) },
        onFocus: (event: Event) => { console.log(`onFocus:${event}`) },
        onBlur: (event: Event) => { console.log(`onBlur:${event}`) },
      }
    },
  ]
})
</script>