<template>
    <div id="dasboard">
        <Personal />
        <div class="divider"></div>
        <SkillsSection />
        <div class="divider"></div>
        <EducationSection />
        <div class="divider"></div>
        <ExperienceSection />
    </div>
</template>

<script>
    import Personal from './Personal'
    import SkillsSection from './skills/SkillsSection'
    import EducationSection from './education/EducationSection'
    import ExperienceSection from './experience/ExperienceSection'
    export default {
        name: 'dashboard',
        components: {
            Personal,
            SkillsSection, 
            EducationSection, 
            ExperienceSection,
        },
        data() {
            return {}
        },
        created () {}
    }
</script>
