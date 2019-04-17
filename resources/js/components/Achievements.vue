<template>
    <div>
        <h1 class="font-normal text-3xl text-grey-darkest leading-none mb-12">
            Achievements
        </h1>

        <input
            placeholder="Your API Token"
            v-model="token"
            class="border p-2 rounded w-full mb-8"
            @keyup.enter="fetchAchievements"
        />

        <p class="text-red italic text-sm" v-if="message" v-text="message"></p>

        <ul>
            <li
                :key="index"
                v-for="(achievement, index) in achievements"
                v-text="achievement.text"
            ></li>
        </ul>
    </div>
</template>

<script>
export default {
    data() {
        return { achievements: [], token: "", message: "" };
    },

    methods: {
        fetchAchievements() {
            axios
                .get(
                    `http://birdboard.local/api/achievements?api_token=${
                        this.token
                    }`
                )
                .catch(error => {
                    this.message = error.message;
                    this.achievements = [];
                })
                .then(({ data }) => {
                    this.achievements = data;
                    this.message = null;
                });
        },
    },
};
</script>
