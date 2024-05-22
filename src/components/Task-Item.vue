<template>
    <div>
        <li>
            <button @click="$emit('complete')" v-bind:class="className">{{ task.title }}</button>
            <button @click="$emit('remove')"><i class="far fa-trash-alt"></i></button>
        </li>
    </div>
    
</template>

<script>

export default ({
    name: 'Task-Item',
    props: ['task'],
    computed: {
        className() {
            let classes = ['toggle'];
            if (this.task.completed) {
                classes.push('toggle-completed');
            }
            return classes;
        }
    }
})
</script>
