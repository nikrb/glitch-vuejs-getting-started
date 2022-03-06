<template>
<div>
    <label>{{track}}</label>
    <label>{{level}}</label>
    <label>{{courseName}}</label>
</div>
</template>

<script>
export default {
    name: "CourseCard",
    props: {
        track: {required: true, type:String},
        level: {required: true, type:Number},
        courseName: {required: true, type:String},
    }
}
</script>

<style>

</style>
