<script>
import AFormItem from 'ant-design-vue/es/form/FormItem'
import DatePicker from 'ant-design-vue/es/date-picker'
import Util from '@/util/base'

export default {
  name: 'SRangePicker',
  inheritAttrs: false,
  methods: {
    /**
     * @description 绑定作用域
     * @param {Object} obj
     * @returns {Object}
     */
    handleScope (obj) {
      const scope = { ...obj }
      const names = Object.keys(obj)
      for (const name of names) {
        if (Util.isFunction(scope[name])) {
          scope[name] = scope[name].bind(this)
        }
      }
      return scope
    }
  },
  render () {
    const label = this.$attrs.label
    const field = this.$attrs.field
    const binds = this.$attrs.binds
    const events = this.$attrs.events
    const decorator = this.$attrs.decorator
    const classAttrs = this.$attrs.binds.class
    const styleAttrs = this.$attrs.binds.style
    const handleScope = this.handleScope

    return (
      <AFormItem label={label}>
        <DatePicker.RangePicker
          ref="component"
          v-decorator={[field, decorator]}
          attrs={handleScope(binds)}
          on={handleScope(events)}
          class={classAttrs}
          style={styleAttrs}
        />
      </AFormItem>
    )
  }
}
</script>

<style lang="less">
[off-disabled] {
  .ant-input[disabled],
  .ant-input-disabled {
    color: rgba(0, 0, 0, 0.65);
    background-color: #ffffff;
    cursor: default;
    opacity: 1;
    & + .ant-calendar-picker-icon {
      cursor: default;
    }
  }
}
</style>
