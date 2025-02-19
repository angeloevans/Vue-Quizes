<script setup>
    import Question from '../components/Question.vue';
    import QuizHeader from '../components/QuizHeader.vue';
    import Result from '../components/Result.vue';
    import { useRoute } from 'vue-router';
    import { ref, computed } from 'vue';
    import quizes from '../data/quizes.json'


    const route = useRoute()    // Route
    const quizId = parseInt(route.params.id)        // Get the ID from route Quiz    
    const quiz = quizes.find(q => q.id === quizId)  // Get the Quiz ID
    const currentQuestionIndex =  ref(0)             // Set the Index to 0
    const numberOfCorrectAnswers = ref(0)
    const showResults= ref(false)


    const questionStatus = computed(()=>  `${currentQuestionIndex.value}/${quiz.questions.length}`) // compute the changes from questionStatus when currentQuestionIndex.value changes
    const barPercentage = computed(()=>  `${currentQuestionIndex.value/quiz.questions.length * 100}%`) // Cumpute the BAR lenght value
    const onOptionSelected = (isCorrect) => {
        if(isCorrect){
            numberOfCorrectAnswers.value++
        }
        if(quiz.questions.length -1 === currentQuestionIndex.value){  // lenght start with 0 while index starts with 1 so we -1 on lenght for looping
            showResults.value = true
        }
        currentQuestionIndex.value++    // Add one to Index of Questions to move to the next
    }
</script> 

<template>
    <div>
        <QuizHeader 
        :questionStatus="questionStatus"
        :barPercentage = "barPercentage"
        />
    </div>    
    <div>
        <Question 
            v-if="!showResults"
            :question="quiz.questions[currentQuestionIndex]"
            @selectOption ="onOptionSelected"
        />  <!-- Go to currentQuestion (we set const qurentQuestionIndex =  ref(0) ) from JSON file-->
        <Result 
            v-else 
            :quizquestionLength = quiz.questions.length
            :numberOfCorrectAnswers="numberOfCorrectAnswers"
        />
    </div>
    <button @click="currentQuestionIndex++">Next Question</button>       
</template>
