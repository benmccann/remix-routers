<script setup lang="ts">
import {
  Link,
  Outlet,
  useLocation,
  useMatches,
  useNavigate,
  useNavigation,
  useNavigationType,
} from "remix-router-vue";
import { computed } from "vue";

const links = {
  Index: "/",
  Parent: "/parent",
  Child: "/parent/child",
  Redirect: "/redirect?location=%2Fparent%2Fchild",
  "Loader Error": "/error?type=loader",
  "Render Error": "/error?type=render",
  "Nested Loader Error": "/parent/error?type=loader",
  "Nested Render Error": "/parent/error?type=render",
  Tasks: "/tasks",
};
const hooks = computed(() => ({
  navigationType: JSON.stringify(useNavigationType().value),
  location: JSON.stringify(useLocation().value),
  navigation: JSON.stringify(useNavigation().value),
  matches: JSON.stringify(useMatches().value),
}));
const navigate = useNavigate();
</script>

<template>
  <h1>Root Layout</h1>
  <nav>
    <Link v-for="(href, text) in links" :key="href" :to="href">{{ text }}</Link>
    <button id="back" @click="() => navigate(-1)">Go Back</button>
  </nav>
  <p v-for="(v, k) in hooks" :key="k">
    {{ k }}():
    <code :id="k">{{ v }}</code>
  </p>
  <Outlet />
</template>
