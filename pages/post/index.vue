<template>
	<div>

		<main>

			<section class="sec sec01">
				
				<div class="inner max800">

					<dl>
						<dt>&nbsp;</dt>
						<dd>
							<input id="post_title" type="text" placeholder="タイトル" />
							<!-- <p class="error" v-if="artTitleError">{{artTitleError}}</p> -->
						</dd>

						<dt>&nbsp;</dt>
						<dd>
							<ul id="post_cat">
								<li>
									<em class="icon-minus"></em><b>カテゴリ4</b>
								</li>
								<li>
									<em class="icon-minus"></em><b>カテゴリ3</b>
								</li>
								<li>
									<em class="icon-minus"></em><b>カテゴリ2</b>
								</li>
								<li>
									<em class="icon-minus"></em><b>カテゴリ1</b>
								</li>
							</ul>
						</dd>

						<dt id="insertEditor">&nbsp;</dt>
						<dd id="code-wrap">
							<textarea id="post_content"></textarea>
							<!-- <p class="error" v-if="artContentError">{{artContentError}}</p> -->
						</dd>
					</dl>
					
					<canvas id="canvas" width="0" height="0"></canvas>
					<input id="ui_image" type="file">

				</div>
			</section>

		</main>


		<nav class="floating-menu pos_btm-right">
			<ul>
				<li id="btn-release" class="trig-lg btn-orange" @click="post_publish">
					<span>
						<b>公開</b>
					</span>
				</li>
				<li id="btn-submenu" class="trig-md" @click="post_draft">
					<span>
						<b>下書き<br />保存</b>
					</span>
				</li>
			</ul>
		</nav>

		<div class="floating-menu pos_top-left">
			<ul>
				<li class="trig-md btn-gray">
					<span>
						<b>記事<br />管理</b>
					</span>
				</li>
			</ul>
		</div>

	</div>
</template>


<script>

/*
if (process.browser) {
  require('~/assets/js/simplemde.js');
  require('~/assets/js/marked.js');
  require('~/assets/js/nailthumb.js');
  require('~/assets/js/post.js');

  require('~/assets/css/simplemde.css');
  require('~/assets/css/nailthumb.css');
}
*/

export default {

	head () {
		return {
			title: '投稿',
			titleTemplate: '%s - RAKUN',
			script: [
				
			],
			link: [
				
			]
		
		} 
	},

	mounted(){
		this.$store.dispatch("init_post")
	},

	methods: {

// 公開
		post_publish(e){
			this.$axios.$post('/article_management/post_publish',
			{
				params:{
					login_account_name: "yamada307",
					title: "あいうえお",
					tag: [
						{
							"tag": "お気に入りTag"
						}
					],
					body: "1234567890qazwsxedcrfvtgbyhnujmik,ol.p;/テスト１テスト２テスト３",
					language: 1
				}
			})
			.then((res) => {
				console.log(res.data);
			})
		},

// 下書き
		post_draft(e){
			this.$axios.$post('/article_management/post_draft',
			{
				params:{
					login_account_name: "yamada307",
					title: "あいうえお",
					tag: [
						{
							"tag": "お気に入りTag"
						}
					],
					body: "1234567890qazwsxedcrfvtgbyhnujmik,ol.p;/テスト１テスト２テスト３",
					language: 1
				}
			})
			.then((res) => {
				console.log(res.data);
			})
		}


	}

}

</script>


<!-- <style scoped> -->
<style>

@import "~/assets/css/post.css"

</style>