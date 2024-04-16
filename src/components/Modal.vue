
<template>
    <Transition name="modal">
        <div class="modal" @click="closeModal">

            <div class="modal__block" @click.stop="">
                <h2 class="modal__block_title">
                    {{ edit ? $t('changeNote') : $t('addNote') }}</h2>
                <div class="modal__block_inputs">
                    <label>
                        <span>Title</span>
                        <input autofocus v-model="title" type="text">
                    </label>
                    <label>
                        <span>Content</span>
                        <textarea v-model="text"></textarea>
                    </label>
                </div>
                <div class="modal__block_btns">
                    <button @click="closeModal" class="modal__block_btns-btn del">{{ $t('cancel') }}</button>
                    <button v-if="!edit" class="modal__block_btns-btn edit" @click="addNote">{{ $t('add') }}</button>
                    <button v-else class="modal__block_btns-btn edit" @click="changeNote">{{ $t('change') }}</button>
                </div>
            </div>
        </div>
    </Transition>
</template>

<script>

import { v4 as uuidv4 } from 'uuid';

export default {
    props: {
        edit: {
            typeof: Boolean,
        },
        editedNote: {
            typeof: Object
        }
    },
    data() {
        return {
            title: '',
            text: ''
        }
    },
    methods: {
        closeModal() {
            this.$emit('close')
            this.title = this.text = ''
        },

        changeNote() {
            if (this.text.length > 2 && this.title.length > 2) {
                const newEditedNote = {
                    id: this.editedNote.id,
                    title: this.title,
                    text: this.text,
                    date: new Date().toLocaleDateString()
                }
                this.$emit('changedNote', newEditedNote)
                this.closeModal()
            }
        },
        addNote() {
            if (this.title != '' && this.text != '') {
                const note = {
                    id: uuidv4(),
                    title: this.title,
                    text: this.text,
                    date: new Date().toLocaleDateString()
                }
                this.$emit('addNote', note)
                this.closeModal()
            }

        }
    }
}
</script>
