<script lang="ts">
import type { LoaderFunction } from "@remix-run/router";
import { useLoaderData } from "remix-router-vue";

import { getTasks } from "~/tasks";
import { sleep } from "~/utils";

export const loader: LoaderFunction = async ({ params }) => {
  await sleep();
  return {
    task: getTasks().find((t) => t.id === params.id),
  };
};
</script>

<script setup lang="ts">
const data = useLoaderData();
</script>

<template>
  <h3>Task</h3>
  <p>
    {{ data.task.task }}
  </p>
</template>
