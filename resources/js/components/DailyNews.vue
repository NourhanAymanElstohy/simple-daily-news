<template>
    <div class="container">
        <div class="row mb-3">
            <h2 class="text-center">Daily News</h2>
        </div>

        <div  v-for="agency in agencies" :key="agency.__id">
            <div class="row mb-1">
                <h5 class="text-danger">Agency: <strong class="text-dark">{{ agency.name }}</strong></h5>
            </div>
            <div class="row">
                <div v-for="(news,i) in agency.latest_news" :key="i" >
                    <b-card
                        :title="news.title"
                        img-src="https://picsum.photos/200/100/?image=20"
                        img-alt="Image"
                        img-top
                        tag="article"
                        style="max-width: 21rem;"
                        class="mb-2 ml-3"
                    >
                        <b-card-text>
                            {{ news.content }}
                        </b-card-text>
                        <p>Rating: {{ news.rating }}</p>
                        <p><i class="fa fa-calendar-alt text-secondary"></i> {{ new Date(news.datetime) | moment("ddd, D MMM YYYY, h:mm:ss a") }}</p>
                    </b-card>
                </div>
            </div>
            <hr>
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            agencies: []
        }
    },
    created() {
        this.axios
            .get('http://localhost:8000/api/daily-news/')
            .then(response => {
                this.agencies = response.data;
                console.log(this.agencies);
            });
    },
}
</script>