<script lang="ts">
import { GithubOutlined, StarOutlined } from '@ant-design/icons-vue';
import { onMounted, ref } from 'vue';

export default {
    name: 'Header',
    components: {
        GithubOutlined,
        StarOutlined,
    },
    setup(props) {
        let stars = ref<number | null>(null);
        onMounted(async () => {
            const repoOwner = "huchenlei";
            const repoName = "sd-webui-openpose-editor";

            try {
                const response = await fetch(`https://api.github.com/repos/${repoOwner}/${repoName}`);
                if (response.ok) {
                    const data = await response.json();
                    stars.value = data.stargazers_count;
                } else {
                    console.error("Failed to fetch star count from GitHub");
                }
            } catch (error) {
                console.error("Error fetching star count:", error);
            }
        });

        return {
            stars,
        };
    },
};
</script>

<template>
</template>
