<template>
    <div class="container">
        <div class="row mb-4 mt-2">
            <div class="col-3">
                 <h2 >Daily News</h2>
            </div>
            <div class="col-6"></div>
            <div class="col-3">
                <b-dropdown id="dropdown-1" text="Sort By" class="">
                    <b-dropdown-item @click="sortNews('rating')">Rating {{ this.sortRate == 'asc' ? 'Ascending' : 'Descending'}}</b-dropdown-item>
                    <b-dropdown-item @click="sortNews('datetime')">Date Time {{ this.sortDate == 'asc' ? 'Ascending' : 'Descending'}}</b-dropdown-item>
                </b-dropdown>
            </div>
        </div>

        <div v-for="agency in agencies" :key="agency.__id">
            <div class="mb-2">
                <h5 class="text-danger">Agency: <strong class="text-dark">{{ agency.name }}</strong></h5>
            </div>
            <div class="row">
                <div v-for="(news,i) in agency.latest_news" :key="i" >
                    <b-card
                        :title="news.title"
                        img-src="https://picsum.photos/300/150/?image=20"
                        img-alt="Image"
                        img-top
                        tag="div"
                        style="max-width: 20rem;"
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
            agencies: [],
            sortRate: 'asc',
            sortDate: 'asc',
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
    methods: {
        sortNews(sortBy){
            if(sortBy == 'rating'){
                this.agencies.forEach(agency => {
                    agency.latest_news.sort((a,b) => {
                        if(this.sortRate == 'asc') {
                            return parseFloat(a.rating) - parseFloat(b.rating);
                        }
                        else if(this.sortRate == 'desc') {
                            return parseFloat(b.rating) - parseFloat(a.rating);
                        }
                    })
                });
                if(this.sortRate == 'asc') this.sortRate = 'desc';
                else this.sortRate = 'asc';
                
            }else if(sortBy == 'datetime'){
                this.agencies.forEach(agency => {
                    agency.latest_news.sort((a,b) => { 
                        if(this.sortDate == 'asc'){
                            return new Date(a.datetime) - new Date(b.datetime);
                        }else if(this.sortDate == 'desc'){
                            return new Date(b.datetime) - new Date(a.datetime);
                        }
                        
                    })
                });
                if(this.sortDate == 'asc') this.sortDate = 'desc';
                else this.sortDate = 'asc';
            }
        }
    }
}
</script>