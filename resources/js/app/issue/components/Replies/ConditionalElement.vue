<template>
    <fade-transition>
        <div v-show="isVisible">
            <slot></slot>
        </div>
    </fade-transition>
</template>

<script>
    import inViewport from 'in-viewport'
    import { EventBus } from '../../../../event-bus.js'
    import { FadeTransition } from 'vue2-transitions'

    export default {
        components: {
            FadeTransition
        },

        props: {
            'whenHidden': {
                type: String
            },
            'parent': {
                type: String
            }
        },

        data() {
            return {
                isVisible: false
            }
        },

        mounted() {
            EventBus.$on('scrollIssue', this.checkDisplay);
        },

        methods: {
             // Check the element is on the parent.
            checkDisplay() {
                this.isVisible = !inViewport(document.querySelector(this.whenHidden), { container: document.querySelector(this.parent) });
            }
        }
    }
</script>
