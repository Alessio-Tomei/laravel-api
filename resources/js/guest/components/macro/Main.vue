<template>
<main>
    <div class="container">
        <section>
            <div class="cards-container">
                <div class="card" v-for="(post, index) in posts" :key="index">
                    <div class="img-container">
                        <img :src=" '../storage/' + post.image" alt="">
                    </div>
                    <h3>Titolo: {{post.title}}</h3>
                    <p>Content: {{post.content}}</p>
                    <p>Category: {{post.category ? post.category.name : '-'}}</p>
                    <p v-if="post.tags.length > 0">
                        Tags:
                        <span v-for="(tag, index) in post.tags" :key="index">{{' - ' + tag.name}}</span>
                    </p>
                    <p v-else>Tags: - </p>
                </div>
            </div>
        </section>
    </div>    
</main>
</template>

<script>
export default {
    name: 'Main',
    data() {
        return {
            posts: [],
        }
    },
    methods: {
        getPosts: function() {
            axios.get('api/posts')
            .then(apiResponse => {
                this.posts = apiResponse.data;
                })
            .catch(() => {
                console.log('error');
            });
        }  
    },
    created() {
        this.getPosts();
    }
}    
</script>

<style lang="scss" scoped>
.img-container {
    width: 200px;
    height: 200px;
    background: gray;
    img {
        width: 100%;
    }
}

</style>