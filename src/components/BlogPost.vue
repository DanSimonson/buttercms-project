<script>
    import butter from '@/buttercms'

    export default {
        name: 'blog-post',
        data() {
            return {
                post: {}
            }
        },
        methods: {
            getPost() {
                butter.post.retrieve(this.$route.params.slug)
                    .then((res) => {
                        console.log(res.data)
                        this.post = res.data
                    }).catch((res) => {
                        console.log(res)
                    })
            }
        },
        watch: {
            $route(to, from) {
                this.getPost()
            }
        },
        created() {
            this.getPost()
            /*var url = "https://mariposaweb.net"
            var slug = window.location.pathname;
            var urlSlug = url + slug;
            console.log(urlSlug);*/
        }
    }
</script>
<template>
    <div>
        <div id="blog-post">
            <app-header></app-header>
            <div id='spacing'></div>
            <h1>{{ post.data.title }}</h1>
            <h4>{{ post.data.author.first_name }} {{ post.data.author.last_name }}</h4>
            <div v-html="post.data.body"></div>

            <router-link style="text-decoration: none" v-if="post.meta.previous_post" :to="/blog/ + post.meta.previous_post.slug" class="button">
                <!--{{ post.meta.previous_post.title }}-->Previous&nbsp
            </router-link>
            <router-link style="text-decoration: none" v-if="post.meta.next_post" :to="/blog/ + post.meta.next_post.slug" class="button">
                <!--{{ post.meta.next_post.title }}-->Next
            </router-link>
        </div>


    </div>
</template>
<style>
    #blog-post {
        font-size: 20px;
    }

    #spacing {
        height: 100px;
    }
</style>