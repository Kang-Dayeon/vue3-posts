<template>
	<div>
		<h2>POST LIST</h2>
		<hr class="my-4" />
		<div class="row">
			<div v-for="post in posts" :key="post.id" class="col-4 g-3">
				<PostItem
					:title="post.title"
					:content="post.content"
					:createdAt="post.createdAt"
					@click="goPage(post.id)"
				></PostItem>
			</div>
		</div>
	</div>
</template>

<script setup>
import { getPosts } from '@/api/posts';
import PostItem from '@/components/posts/PostItem.vue';
import { ref } from 'vue';
import { useRouter } from 'vue-router';

const posts = ref([]);

const fetchPosts = () => {
	posts.value = getPosts();
};

fetchPosts();

const router = useRouter();
const goPage = id => {
	router.push({
		name: 'PostDetail',
		params: {
			id,
		},
	});
};
</script>

<style lang="scss" scoped></style>
