<template>
	<div class="speach-component">
		<h1>Genius robot</h1>

		<button @click="startRecognition()">Start it!</button>

		<br><br>

		<hr>

		<div class="results">
			
			<h2 class="answer">{{ answer }}</h2>

			<hr>
			<div class="heard">
				<p>I've heard: </p>
				<h3>{{ lastResult }}</h3>
				<p>{{ lastConfidence }}</p>
			</div>
		</div>
	</div>
</template>
<script>

export default {
	name: 'speach',
	data: ()=>{
		return {
			recognition: null,
			lastResult: '',
			lastConfidence: '',
			answer: 'Talk to me baby'
		}
	},

	methods:{
		startRecognition(){
			this.recognition.start();
			console.log( 'Ready to start receiving commands!' );
		},

		resultFound(e){
			//console.log( e );
			var last = e.results.length - 1;
			this.lastResult = e.results[last][0].transcript;
			this.lastConfidence = e.results[0][0].confidence;

			this.clear();
			this.matcher( this.lastResult );
		},

		awesome(){
			this.answer = 'Well thank you!';
		},

		shit(){
			this.answer = 'screw you too!'
		},

		clear(){
			this.answer = 'Talk to me baby'
		},


		matcher(resultString){
			

			var resultsLowercase = resultString.toLowerCase();
			var invocation = 'genius '

			console.log( resultsLowercase );

			var match = '';

			// awesome
			match = invocation + 'you are awesome';
			if ( resultsLowercase.indexOf( match ) !== -1 ){
				this.awesome();
			}
			
			// awesome
			match = 'you are awesome genius';
			if ( resultsLowercase.indexOf( match ) !== -1 ){
				this.awesome();
			}

			// suck
			match = invocation + 'you suck';
			if ( resultsLowercase.indexOf( match ) !== -1 ){
				this.shit();
			}


		}
	},

	mounted(){
		var SpeechRecognition = SpeechRecognition || webkitSpeechRecognition
		//var SpeechGrammarList = SpeechGrammarList || webkitSpeechGrammarList
		var SpeechRecognitionEvent = SpeechRecognitionEvent || webkitSpeechRecognitionEvent

		//var colors = [ 'red', 'green', 'blue' ];
		//var grammar = '#JSGF V1.0; grammar colors; public <color> = ' + colors.join(' | ') + ' ;'

		this.recognition = new SpeechRecognition();
		//var speechRecognitionList = new SpeechGrammarList();

		//speechRecognitionList.addFromString(grammar, 1);
		//this.recognition.grammars = speechRecognitionList;

		this.recognition.lang = 'en-US';
		this.recognition.continuous = true;
		//this.recognition.interimResults = true;

		this.recognition.onresult = this.resultFound;


	}
}

</script>
<style>
.answer{
	font-size: 48px;
}

</style>