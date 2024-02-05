<template>
  <div class="p-10">
    <span>Card: {{ counter.count }}/{{ cards.length }}</span>
    <div class="overflow-hidden mt-2 rounded-lg bg-gray-100 py-2 shadow sm:p-6 mb-2 card-image">
      <div class="mt-3 mb-3">
        <h3 class="font-bold text-xl border-b border-gray-200 dark:border-gray-200 pb-2 pl-2">
          {{ currentCard.topic }}
        </h3>
        <div class="px-4 mt-3">
          <ul class="">
            <li
              v-for="(question, index) in currentCard.questions"
              class="w-full px-4 py-2 border-b border-gray-200 dark:border-gray-600"
              :key="index"
            >
              {{ question }}
            </li>
          </ul>
        </div>

        <div class="inline-flex mt-4 ml-3 rounded-md shadow-sm" role="group">
          <button
            type="button"
            @click="previousCard"
            :disabled="counter.count == 1"
            class="px-4 py-2 text-sm font-medium text-blue-900 bg-white border border-gray-200 rounded-s-lg hover:bg-gray-100 hover:text-blue-700 focus:z-10 focus:ring-2 focus:ring-blue-700 focus:text-blue-700 dark:bg-blue-700 dark:border-blue-600 dark:text-white dark:hover:text-white dark:hover:bg-gray-600 dark:focus:ring-blue-500 dark:focus:text-white"
          >
            Previous
          </button>
          <button
            type="button"
            @click="nextCard"
            :disabled="counter.count == cards.length"
            class="px-4 py-2 text-sm font-medium text-blue-900 bg-white border border-gray-200 rounded-e-lg hover:bg-gray-100 hover:text-blue-700 focus:z-10 focus:ring-2 focus:ring-blue-700 focus:text-blue-700 dark:bg-blue-700 dark:border-blue-600 dark:text-white dark:hover:text-white dark:hover:bg-gray-600 dark:focus:ring-blue-500 dark:focus:text-white"
          >
            Next
          </button>
        </div>
      </div>
    </div>
  </div>

  <RouterView />
</template>

<script setup lang="ts">
import { reactive } from 'vue'
// import { RouterLink, RouterView } from 'vue-router'

type Card = {
  topic: string
  questions: string[]
}

const counter = reactive({
  count: 1
})

const nextCard = () => {
  counter.count++
  changeCard()
}
const previousCard = () => {
  counter.count--
  changeCard()
}

const cards: Card[] = [
  {
    topic: 'Emotional Well-being',
    questions: [
      'How have you been feeling emotionally lately?',
      "Is there anything on your mind or heart that you'd like to share?",
      'How can I support you better in managing stress or challenges?'
    ]
  },
  {
    topic: 'Communication',
    questions: [
      "Are there any topics or issues that you feel we haven't been communicating about effectively?",
      'Do you feel heard and understood in our conversations?',
      'Is there anything you think we could do to improve our communication as a couple?'
    ]
  },
  {
    topic: 'Quality Time',
    questions: [
      'Have we been spending enough quality time together recently?',
      "Is there a particular activity or outing you'd like to do together soon?",
      'How can we ensure we prioritize our relationship amidst our other commitments?'
    ]
  },
  {
    topic: 'Intimacy',
    questions: [
      'How satisfied are you with the level of intimacy in our relationship?',
      "Are there any changes or improvements you'd like to see in this area?",
      'What can we do to keep the spark alive and nurture our physical and emotional connection?'
    ]
  },
  {
    topic: 'Shared Goals and Values',
    questions: [
      'Are we still aligned in terms of our long-term goals and values?',
      "Do you have any new goals or aspirations that you'd like to share with me?",
      'How can we continue to support each other in pursuing our individual and shared dreams?'
    ]
  },
  {
    topic: 'Appreciation and Affection',
    questions: [
      'What are some things you appreciate about our relationship right now?',
      "Is there something specific I've done recently that made you feel loved or valued?",
      'How can we express gratitude and affection towards each other more consistently?'
    ]
  },
  {
    topic: 'Resolving Conflict',
    questions: [
      'Have there been any unresolved issues or conflicts between us that need addressing?',
      'How do you think we can approach conflict resolution more effectively in the future?',
      'Are there any patterns in our disagreements that we should be aware of and work on?'
    ]
  },
  {
    topic: 'Future Plans',
    questions: [
      'How do you envision our relationship evolving in the future?',
      'Are there any big decisions or changes on the horizon that we should discuss?',
      'What steps can we take together to ensure our relationship continues to grow and thrive?'
    ]
  }
]

const currentCard: Card = reactive({
  topic: cards[0].topic,
  questions: cards[0].questions
})

const changeCard = () => {
  const currentCount = counter.count - 1
  currentCard.topic = cards[currentCount].topic
  currentCard.questions = cards[currentCount].questions
}
</script>
