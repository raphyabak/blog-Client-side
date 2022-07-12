<template>
    <section class="bg-white dark:bg-gray-900">
        <div class="py-8 px-4 mx-auto max-w-screen-xl lg:py-16 lg:px-6">
            <div class="max-w-screen-lg text-gray-500 sm:text-lg dark:text-gray-400">
                <h2 class="mb-4 text-4xl tracking-tight font-bold text-gray-900 dark:text-white">{{ post.title }}</h2>
                <div class="mb-4 font-light prose lg:prose-xl" v-html="post.body"></div>
            </div>
        </div>
    </section>
</template>

<script>
import { onMounted } from 'vue'
import usePosts from '../api/usePosts'
export default {

    props: {
        slug: {
            required: true,
            type: String
        }
    },

    setup(props) {
        const { post, fetchPost } = usePosts()

        onMounted(fetchPost(props.slug))

        return {
            post
        }
    },
}
</script>