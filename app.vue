<template>
	<!--  Pop Up Component  -->
	<pop-up
		v-if="announceStatus === false"
		@closen="changeAnnounceStatus"
		:data="popUpData"
	/>

	<!--  Sticky Happy Face  -->
	<div
		class="fixed bottom-0 right-0 z-[99] mx-5 md:mx-[4rem] my-5 md:my-13 xl:my-20 cursor-pointer"
	>
		<div class="sticky">
			<a href="#budget">
				<div v-if="selectImage" class="absolute top-[-70px] right-[40px]">
					<nuxt-img
						src="/images/soyFelizStudio/happy-face-hover.png"
						alt="soy feliz studio"
						class="max-w-[120px]"
						format="webp"
					/>
				</div>
				<nuxt-img
					@mouseleave="leaveFace($viewport.isGreaterOrEquals('desktop'))"
					@mouseover="hoverFace($viewport.isGreaterOrEquals('desktop'))"
					src="/images/soyFelizStudio/happy-face.png"
					alt="soy feliz studio"
					class="max-w-[60px]"
					format="webp"
				/>
			</a>
		</div>
	</div>

	<!-- Navigation Bar -->
	<navigation-bar />

	<!--  Video Component  -->
	<section
		v-if="videoUrl"
		class="lg:mt-10 h-[90vh] max-w-5xl lg:mx-auto lg:h-[36rem] scroll-mt-[110px]"
		id="home"
	>
		<iframe
			allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share"
			:src="videoUrl"
			class="w-full h-full"
			frameborder="0"
		/>
	</section>

	<!--  We Component  -->
	<section class="scroll-mt-[70px]" id="we">
		<we />
	</section>

	<!--  Galery Component  -->
	<section class="scroll-mt-[70px]" id="galery">
		<instagram-feed />
	</section>

	<!--  Artist Component  -->
	<section class="scroll-mt-[70px]" id="artists">
		<artist />
	</section>

	<!--  Budget Component  -->
	<section class="scroll-mt-[70px]" id="budget">
		<budget @closen="changeAnnounceStatus" />
	</section>

	<!--  COntact Component  -->
	<section class="scroll-mt-[-20px]" id="contact">
		<contact />
	</section>
</template>

<script lang="ts">
import { defineComponent, ref } from 'vue'

import NavigationBar from './components/navigation-bar.vue'
import InstagramFeed from './components/instagram-feed.vue'
import Contact from './components/contact.vue'
import Artist from './components/artists.vue'
import Budget from './components/budget.vue'
import PopUp from './components/pop-up.vue'
import We from './components/we.vue'

export default defineComponent({
	components: {
		InstagramFeed,
		NavigationBar,
		Contact,
		Budget,
		Artist,
		PopUp,
		We,
	},

	setup() {
		const config = useRuntimeConfig()

		const announceStatus = ref(true)

		const popUpData = ref('home')
		const changeAnnounceStatus = (data: string) => {
			announceStatus.value = !announceStatus.value
			if (data) popUpData.value = data
		}

		const selectImage = ref(false)

		const videoUrl = ref(config.public.VIDEO_URL)

		const hoverFace = (width: boolean) => {
			if (width) selectImage.value = true
		}

		const leaveFace = (width: boolean) => {
			if (width) selectImage.value = false
		}

		return {
			changeAnnounceStatus,
			announceStatus,
			selectImage,
			hoverFace,
			leaveFace,
			popUpData,
			videoUrl,
		}
	},
})
</script>
