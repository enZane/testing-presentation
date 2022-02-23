<template>
  <div>
    <div class="container max-w-800px mx-auto py-6">
      <!-- Output Box -->
      <div class="border border-gray-300 rounded-lg p-3">
        <div class="relative flex flex-col items-end">
          <svg
            focusable="false"
            xmlns="http://www.w3.org/2000/svg"
            viewBox="0 0 24 24"
            class="hover:fill-purple-500 w-5 text-gray-500 fill-current absolute top-0 left-0"
          >
            <path
              d="M13 3a9 9 0 0 0-9 9H1l3.89 3.89.07.14L9 12H6c0-3.87 3.13-7 7-7s7 3.13 7 7-3.13 7-7 7c-1.93 0-3.68-.79-4.94-2.06l-1.42 1.42A8.954 8.954 0 0 0 13 21a9 9 0 0 0 0-18zm-1 5v5l4.28 2.54.72-1.21-3.5-2.08V8H12z"
            />
          </svg>

          <div class="text-xs text-gray-500 mb-1">
            <span v-show="calcResult.length > 0">{{ calcString2 }} = {{ calcResult }}</span>
          </div>
          <div class="text-3xl">
            <span>{{ calcString }}</span>
          </div>
        </div>
      </div>
      <!-- Numpad -->
      <div class="mt-2 -mx-1">
        <table class="w-full table-fixed">
          <tr>
            <td colspan="3" />
            <td>
              <button
                class="rounded-md bg-gray-200 h-10 w-full text-center"
                @click="clearInput()"
              >CE</button>
            </td>
          </tr>
          <tr>
            <td>
              <Button button="7" @input="input(7)" />
            </td>
            <td>
              <Button button="8" @input="input(8)" />
            </td>
            <td>
              <Button button="9" @input="input(9)" />
            </td>
            <td>
              <Button button="+" operator @input="input('+')" />
            </td>
          </tr>
          <tr>
            <td>
              <Button button="4" @input="input(4)" />
            </td>
            <td>
              <Button button="5" @input="input(5)" />
            </td>
            <td>
              <Button button="6" @input="input(6)" />
            </td>
            <td>
              <Button button="x" operator @input="input('x')" />
            </td>
          </tr>
          <tr>
            <td>
              <Button button="1" @input="input(1)" />
            </td>
            <td>
              <Button button="2" @input="input(2)" />
            </td>
            <td>
              <Button button="3" @input="input(3)" />
            </td>
            <td>
              <Button button="-" operator @input="input('-')" />
            </td>
          </tr>
          <tr>
            <td>
              <Button button="0" @input="input(0)" />
            </td>
            <td>
              <Button button="." operator @input="input('.')" />
            </td>
            <td>
              <Button button="=" operator @input="submit()" />
            </td>
            <td>
              <Button button="+" operator @input="input('+')" />
            </td>
          </tr>
        </table>
      </div>
    </div>
  </div>
</template>

<script>
import { evaluate } from "mathjs";
import Button from "./Button.vue";
export default {
  name: "Calculator",
  data() {
    return {
      outputNum: "",
      calcString: "0",
      calcString2: "",
      calcResult: "",
      operationSet: false,
    };
  },
  methods: {
    input(num) {
      this.calcString =
        this.calcString === "0" ? num : `${this.calcString}${num}`;
    },
    inputDecimal(decimal) {
      let inputNumbers = this.calcString
        .toString()
        .split("x")
        .join(", ")
        .split("+")
        .join(", ")
        .split("÷")
        .join(", ")
        .split("-")
        .join(", ");
      inputNumbers = inputNumbers.split(",");
      if (inputNumbers[inputNumbers.length - 1].indexOf(decimal) > -1)
        return;
      this.calcString = this.calcString + decimal;
    },
    clearInput() {
      this.calcString =
        this.calcString.length === 1
          ? "0"
          : this.calcString.substring(0, this.calcString.length - 1);
    },
    submit() {
      let evalString = this.calcString.replace(/x/g, "*").replace(/÷/g, "/");
      this.calcString2 = this.calcString;
      this.calcResult = evaluate(evalString).toString();
      this.calcString = evaluate(evalString).toString();
    },
  },
  components: { Button }
};
</script>

<style scoped>
table td {
  @apply p-1;
}
</style>