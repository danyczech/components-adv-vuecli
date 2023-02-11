<template>
  <div>
    <TheHeader />
    <BadgeList />
    <UserInfo
      :full-name="activeUser.name"
      :info-text="activeUser.description"
      :role="activeUser.role"
    ></UserInfo>
    <CourseGoals #default="slotProps">
      <h2> {{ slotProps.item }}</h2>
      <p>{{ slotProps['anotherprop'] }}</p>
     
      <!-- universal template, if it is default slot and the only one , can be shortened
      <template #default="slotProps">
        <h2> {{ slotProps.item }}</h2>
        <p>{{ slotProps['anotherprop'] }}</p>
      </template>
      -->
    </CourseGoals>

    <button @click="setSelectedComponent('ManageGoals')">Manage Goals</button>
    <button @click="setSelectedComponent('ActiveGoals')">Active Goals</button>
    <ManageGoals></ManageGoals>
    <ActiveGoals></ActiveGoals>

    <keep-alive>
      <component :is="selectedComponent"></component>
    </keep-alive>
    
  </div>
</template>

<script>
import TheHeader from "./layout/TheHeader.vue"
import BadgeList from "./components/BadgeList.vue"
import UserInfo from "./components/UserInfo.vue"
import CourseGoals from "./components/CourseGoals.vue"
import ManageGoals from "./components/ManageGoals.vue"
import ActiveGoals from "./components/ActiveGoals.vue"

export default {
  components: {
    TheHeader,
    BadgeList,
    UserInfo,
    CourseGoals,
    ManageGoals,
    ActiveGoals
  },
  data() {
    return {
      selectedComponent: 'ActiveGoals',
      activeUser: {
        name: "Maximilian Schwarzmüller",
        description: "Site owner and admin",
        role: "admin",
      },
    }
  },
  methods: {
    setSelectedComponent (cmp) {
      this.selectedComponent = cmp;
    }
  }
}
</script>

<style>
html {
  font-family: sans-serif;
}

body {
  margin: 0;
}
</style>
