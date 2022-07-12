<script>
import { ref } from '@vue/reactivity'
import { onMounted } from '@vue/runtime-core'
export default {
    setup(props, context) {

        const el = ref(null)

        const resizeTarget = (target) => {
            // console.log(target.scrollHeight)
            target.style.height = 'auto'
            target.style.height = `${target.scrollHeight}px`
        }

        const resize = (e) => {
            resizeTarget(e.target)
            // console.log('resize')
        }

        onMounted( function (){
            resizeTarget(el.value)
        })

        return () => context.slots.default({
            resize,
            el
        })

    },
}
</script>