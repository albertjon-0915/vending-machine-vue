<script setup>
import { ref, defineProps, watch } from "vue";

const props = defineProps({
  vendingItems: Array,
});

const keys = [1, 2, 3, 4, 5, 6, 7, 8, 9, "*", 0, "Del"];
const bills = [1000, 500, 100, 50, 20, 10, 5, 1];
const itemNumber = ref(0);
const toPay = ref(0);
const vendingNewArr = ref([...props.vendingItems]);
const owedBill = ref(0);
const isOnItemList = ref(true);
const changeBill = ref("");

const computeChange = () => {
  console.log("compute");

  let change = toPay.value - owedBill.value;
  const changeArr = [];

  console.log(change, changeArr);

  bills.map((item) => {
    const count = Math.floor(change / item);

    if (count > 0) {
      changeArr.push(`${count} - ${item} ${item < 20 ? "coins" : "bills"}, `);
      change -= count * item;
    } else {
      toPay.value = 0;
      owedBill.value = 0;
      itemNumber.value = 0;
    }
  });

  return (changeBill.value = changeArr.join("\n"));
};

watch(itemNumber, (newValue) => {
  const findItem = vendingNewArr.value.find(
    (item) => item.itemNo == itemNumber.value
  );

  if (findItem) return (owedBill.value = findItem.itemPrice);
  if (newValue === 0) return (isOnItemList.value = true);
  if (!findItem) {
    owedBill.value = 0;
    return (isOnItemList.value = false);
  }
});

const keyAction = (item) => {
  if (item === "*") return (itemNumber.value = 0);
  if (item === "Del" && String(itemNumber.value).length > 1)
    return (itemNumber.value = parseInt(
      itemNumber.value.toString().slice(0, -1)
    ));
  if (item === "Del" && String(itemNumber.value).length === 1)
    return (itemNumber.value = 0);

  const newItemNum = parseInt((itemNumber.value += item.toString()));
  return (itemNumber.value = newItemNum);
};

const addToPay = (bill) => {
  const newToPay = (toPay.value += bill);
  return (toPay.value = newToPay);
};

const minusBill = (bill) => {
  if (bill > toPay.value) return;

  const newToPay = (toPay.value -= bill);
  return (toPay.value = newToPay);
};
</script>

<template>
  <div class="keyboardContainer">
    <form @submit.prevent="computeChange">
      <input
        type="text"
        placeholder="input item number"
        @keypress.prevent
        @keyup.prevent
        @keydown.prevent
        :value="itemNumber !== 0 ? itemNumber : ''"
      />
      <button>ok</button>
    </form>
    <div class="payment">
      <div class="errPrompt" v-if="isOnItemList === false">
        <span> X </span>
        Item not on the list
      </div>
      <div>
        Payment: <span class="bill">Php {{ toPay }}</span>
      </div>
      <div>
        Owed:
        <span class="owedBill" v-if="owedBill !== 0 ? true : false"
          >Php {{ owedBill }}</span
        >
      </div>
      <div class="change">
        Change:
        <span> {{ changeBill }}</span>
      </div>
    </div>
    <ul class="keypad">
      <li v-for="key in keys" :key="key">
        <div @click="keyAction(key)">
          <span>{{ key }}</span>
        </div>
      </li>
    </ul>

    <h3>
      Insert bill/coin: <span class="bill">Php {{ toPay }}</span>
    </h3>

    <ul class="coins">
      <li v-for="bill in bills" :key="bill" @click.stop="addToPay(bill)">
        <div>
          <span>{{ bill }}</span>
          <div class="billCount" @click.stop="minusBill(bill)">
            <span>-</span>
          </div>
        </div>
      </li>
    </ul>
  </div>
</template>

<style scoped lang="scss">
.keyboardContainer {
  padding: 2em 0;
  width: 100%;
  height: auto;
}

form {
  display: flex;
  gap: 0.5em;
  height: 5em;

  input,
  button {
    height: 100%;
  }

  input {
    all: unset;
    border: 1px solid #b98800;
    font-size: 1.5em;
    width: 100%;
    padding: 0 2em;
    text-align: right;

    &:focus,
    &:focus-visible,
    &:hover {
      outline: 3px solid #beb41a;
    }

    &::placeholder {
      font-size: clamp(0.65em, 0.8vw, 0.8em);
      color: rgba(185, 136, 0, 0.4);
    }
  }

  button {
    border: none;
    border-radius: 5px;
    box-shadow: -1px 1px 5px 1px #8080804b;
    width: 10em;
    cursor: pointer;
  }
}

.change {
  span {
    font-weight: 700;
    font-size: 1.2em;
    color: #61817f;
  }
}

.errPrompt {
  margin: 0.7em 0;
  background: #e9b7ce;
  padding: 0.2em 1em;
  color: #ffff;

  span {
    color: #ff0037;
  }
}

.payment {
  font-size: 0.85em;
  color: #444444;
  margin-bottom: 3em;
}

.owedBill {
  font-weight: bold;
  font-size: 1.2em;
  color: #ff0037;
}

.bill {
  font-weight: bold;
  font-size: 1.2em;
  color: rgb(104, 173, 0);
}

.keypad {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 1em;
  padding: 3em 1em;
  border-radius: 5px;
  border: 1px solid rgba(128, 128, 128, 0.438);

  li {
    all: unset;
    display: grid;
    place-items: center;

    div {
      display: grid;
      place-content: center;
      width: 5em;
      aspect-ratio: 1 / 1;
      border-radius: 50%;
      border: 1px solid rgba(128, 128, 128, 0.438);
      cursor: pointer;
    }
  }
}

h3 {
  margin: 3em 0 1em 0;
}

.coins {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 1em;

  li {
    all: unset;
    border: 1px solid #80808070;
    padding: 1em;
    cursor: pointer;

    div {
      display: flex;
      justify-content: space-between;

      .billCount {
        font-weight: 900;
        display: flex;

        span {
          padding: 0 0.5em;
          cursor: pointer;
        }
      }
    }
  }
}
</style>
