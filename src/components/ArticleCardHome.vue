<template>
	<div class="my-card">
		<router-link :to="{ name: 'view-article', params: { id: article.id } }">
			<div class="image">
				<img :src="article.image" alt="" />
			</div>
		</router-link>
		<div class="contant">
			<div class="title">
				{{ article.title }}
			</div>
			<div class="summar">
				{{ aaa.length > 100 ? aaa.slice(0, 100) + "..." : aaa }}
			</div>
			<router-link :to="{ name: 'view-article', params: { id: article.id } }">
				<m-button class="slide-button my-btn">اقرأ أكثر</m-button>
			</router-link>
		</div>
	</div>
</template>

<script>
import MButton from "../m-labs/vue/MButton.vue";
export default {
	props: ["article"],
	components: { MButton },
	data() {
		return {
			aaa: `لوريم ايبسوم هو نموذج افتراضي يوضع في التصاميم لتعرض على العميل ليتصور طريقه وضع النصوص بالتصاميم سواء كانت تصاميم مطبوعه ... بروشور او فلاير على سبيل المثال ... او نماذج مواقع انترنت ...
            
            وعند موافقه العميل المبدئيه على التصميم يتم ازالة هذا النص من التصميم ويتم وضع النصوص النهائية المطلوبة للتصميم ويقول البعض ان وضع النصوص التجريبية بالتصميم قد تشغل المشاهد عن وضع الكثير من الملاحظات او الانتقادات للتصميم الاساسي.
            
            وخلافاَ للاعتقاد السائد فإن لوريم إيبسوم ليس نصاَ عشوائياً، بل إن له جذور في الأدب اللاتيني الكلاسيكي منذ العام 45 قبل الميلاد. من كتاب "حول أقاصي الخير والشر"`,
		};
	},
};
</script>

<style scoped lang="scss">
.my-card {
	display: flex;
	align-items: center;
	.image {
		height: 150px;
		width: 150px;
		img {
			height: 100%;
			width: 100%;
			object-fit: cover;
		}
	}
	.contant {
		text-align: right;
		padding-right: 20px;
	}
	.title {
		font-size: 1.3rem;
		font-weight: 600;
	}
	.my-btn {
		margin: 0;
		margin-top: 10px;
		color: var(--accent);
		box-shadow: 0 0 5px var(--accent) inset;
		&::after {
			color: white;
		}
		&:hover {
			color: white;
		}
	}
}
</style>