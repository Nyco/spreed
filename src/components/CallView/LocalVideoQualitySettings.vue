<!--
  - @copyright Copyright (c) 2020, Daniel Calviño Sánchez (danxuliu@gmail.com)
  -
  - @license GNU AGPL version 3 or any later version
  -
  - This program is free software: you can redistribute it and/or modify
  - it under the terms of the GNU Affero General Public License as
  - published by the Free Software Foundation, either version 3 of the
  - License, or (at your option) any later version.
  -
  - This program is distributed in the hope that it will be useful,
  - but WITHOUT ANY WARRANTY; without even the implied warranty of
  - MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
  - GNU Affero General Public License for more details.
  -
  - You should have received a copy of the GNU Affero General Public License
  - along with this program. If not, see <http://www.gnu.org/licenses/>.
  -
  -->

<template>
	<div>
		<div>
			<p>Videos threshold for thumbnail: {{ availableVideosThresholdForThumbnail }}</p>
			<input v-model="availableVideosThresholdForThumbnail"
				type="range"
				min="1"
				max="50"
				@input="updateAvailableVideosThreshold">
			<p>Videos threshold for very low quality: {{ availableVideosThresholdForVeryLowQuality }}</p>
			<input v-model="availableVideosThresholdForVeryLowQuality"
				type="range"
				min="1"
				max="50"
				@input="updateAvailableVideosThreshold">
			<p>Videos threshold for low quality: {{ availableVideosThresholdForLowQuality }}</p>
			<input v-model="availableVideosThresholdForLowQuality"
				type="range"
				min="1"
				max="50"
				@input="updateAvailableVideosThreshold">
			<p>Videos threshold for medium quality: {{ availableVideosThresholdForMediumQuality }}</p>
			<input v-model="availableVideosThresholdForMediumQuality"
				type="range"
				min="1"
				max="50"
				@input="updateAvailableVideosThreshold">
			<p>Videos threshold for high quality: {{ availableVideosThresholdForHighQuality }}</p>
			<input v-model="availableVideosThresholdForHighQuality"
				type="range"
				min="1"
				max="50"
				@input="updateAvailableVideosThreshold">
		</div>
		<div>
			<p>Audios threshold for thumbnail: {{ availableAudiosThresholdForThumbnail }}</p>
			<input v-model="availableAudiosThresholdForThumbnail"
				type="range"
				min="1"
				max="50"
				@input="updateAvailableAudiosThreshold">
			<p>Audios threshold for very low quality: {{ availableAudiosThresholdForVeryLowQuality }}</p>
			<input v-model="availableAudiosThresholdForVeryLowQuality"
				type="range"
				min="1"
				max="50"
				@input="updateAvailableAudiosThreshold">
			<p>Audios threshold for low quality: {{ availableAudiosThresholdForLowQuality }}</p>
			<input v-model="availableAudiosThresholdForLowQuality"
				type="range"
				min="1"
				max="50"
				@input="updateAvailableAudiosThreshold">
			<p>Audios threshold for medium quality: {{ availableAudiosThresholdForMediumQuality }}</p>
			<input v-model="availableAudiosThresholdForMediumQuality"
				type="range"
				min="1"
				max="50"
				@input="updateAvailableAudiosThreshold">
			<p>Audios threshold for high quality: {{ availableAudiosThresholdForHighQuality }}</p>
			<input v-model="availableAudiosThresholdForHighQuality"
				type="range"
				min="1"
				max="50"
				@input="updateAvailableAudiosThreshold">
		</div>
	</div>
</template>

<script>
import { getSentVideoQualityThrottler } from '../../utils/webrtc/index'

export default {

	name: 'LocalVideoQualitySettings',

	data() {
		return {
			sentVideoQualityThrottler: null,

			availableVideosThresholdForThumbnail: 0,
			availableVideosThresholdForVeryLowQuality: 0,
			availableVideosThresholdForLowQuality: 0,
			availableVideosThresholdForMediumQuality: 0,
			availableVideosThresholdForHighQuality: 0,

			availableAudiosThresholdForThumbnail: 0,
			availableAudiosThresholdForVeryLowQuality: 0,
			availableAudiosThresholdForLowQuality: 0,
			availableAudiosThresholdForMediumQuality: 0,
			availableAudiosThresholdForHighQuality: 0,
		}
	},

	mounted() {
		this.sentVideoQualityThrottler = getSentVideoQualityThrottler()

		this.availableVideosThresholdForThumbnail = this.sentVideoQualityThrottler._availableVideosThreshold[this.sentVideoQualityThrottler.QUALITY.THUMBNAIL]
		this.availableVideosThresholdForVeryLowQuality = this.sentVideoQualityThrottler._availableVideosThreshold[this.sentVideoQualityThrottler.QUALITY.VERY_LOW]
		this.availableVideosThresholdForLowQuality = this.sentVideoQualityThrottler._availableVideosThreshold[this.sentVideoQualityThrottler.QUALITY.LOW]
		this.availableVideosThresholdForMediumQuality = this.sentVideoQualityThrottler._availableVideosThreshold[this.sentVideoQualityThrottler.QUALITY.MEDIUM]
		this.availableVideosThresholdForHighQuality = this.sentVideoQualityThrottler._availableVideosThreshold[this.sentVideoQualityThrottler.QUALITY.HIGH]

		this.availableAudiosThresholdForThumbnail = this.sentVideoQualityThrottler._availableAudiosThreshold[this.sentVideoQualityThrottler.QUALITY.THUMBNAIL]
		this.availableAudiosThresholdForVeryLowQuality = this.sentVideoQualityThrottler._availableAudiosThreshold[this.sentVideoQualityThrottler.QUALITY.VERY_LOW]
		this.availableAudiosThresholdForLowQuality = this.sentVideoQualityThrottler._availableAudiosThreshold[this.sentVideoQualityThrottler.QUALITY.LOW]
		this.availableAudiosThresholdForMediumQuality = this.sentVideoQualityThrottler._availableAudiosThreshold[this.sentVideoQualityThrottler.QUALITY.MEDIUM]
		this.availableAudiosThresholdForHighQuality = this.sentVideoQualityThrottler._availableAudiosThreshold[this.sentVideoQualityThrottler.QUALITY.HIGH]
	},

	methods: {

		updateAvailableVideosThreshold() {
			const availableVideosThreshold = {}
			availableVideosThreshold[this.sentVideoQualityThrottler.QUALITY.THUMBNAIL] = this.availableVideosThresholdForThumbnail
			availableVideosThreshold[this.sentVideoQualityThrottler.QUALITY.VERY_LOW] = this.availableVideosThresholdForVeryLowQuality
			availableVideosThreshold[this.sentVideoQualityThrottler.QUALITY.LOW] = this.availableVideosThresholdForLowQuality
			availableVideosThreshold[this.sentVideoQualityThrottler.QUALITY.MEDIUM] = this.availableVideosThresholdForMediumQuality
			availableVideosThreshold[this.sentVideoQualityThrottler.QUALITY.HIGH] = this.availableVideosThresholdForHighQuality

			this.sentVideoQualityThrottler.setAvailableVideosThreshold(availableVideosThreshold)
		},

		updateAvailableAudiosThreshold() {
			const availableAudiosThreshold = {}
			availableAudiosThreshold[this.sentVideoQualityThrottler.QUALITY.THUMBNAIL] = this.availableAudiosThresholdForThumbnail
			availableAudiosThreshold[this.sentVideoQualityThrottler.QUALITY.VERY_LOW] = this.availableAudiosThresholdForVeryLowQuality
			availableAudiosThreshold[this.sentVideoQualityThrottler.QUALITY.LOW] = this.availableAudiosThresholdForLowQuality
			availableAudiosThreshold[this.sentVideoQualityThrottler.QUALITY.MEDIUM] = this.availableAudiosThresholdForMediumQuality
			availableAudiosThreshold[this.sentVideoQualityThrottler.QUALITY.HIGH] = this.availableAudiosThresholdForHighQuality

			this.sentVideoQualityThrottler.setAvailableAudiosThreshold(availableAudiosThreshold)
		},

	},

}
</script>

<style lang="scss" scoped>
</style>
