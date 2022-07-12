<template>
    <EditorContent :editor="editor" />
</template>

<script>
import { useEditor, EditorContent } from '@tiptap/vue-3'
import starterkit from '@tiptap/starter-kit'
import { watch } from 'vue'

export default {

    props: {
        modelValue: {
            type: String,
            default: ''
        },

        teaserValue: {
            type: String,
            default: ''
        }
    },

    components: {
        EditorContent
    },


    setup(props, { emit }) {

        const editor = useEditor({
            content: props.modelValue,
            extensions: [
                starterkit
            ],
            editorProps: {
                attributes: {
                     class: 'min-w-full w-full text-gray-500 prose prose-sm lg:prose focus:outline-none px-2'
                }
            },

            onUpdate: (context) => {
                const teaser = context.editor.state.doc.content.content.find(
                    c => c.type.name === 'paragraph'
                )

                emit('update:teaserValue', teaser.textContent)
                emit('update:modelValue', context.editor.getHTML())
            }

        })

        watch(() => props.modelValue, (value) => {
            if (editor.value.getHTML() === value) {
                return
            }

            editor.value.commands.setContent(props.modelValue)
        })

        return {
            editor
        }

    },
}
</script>