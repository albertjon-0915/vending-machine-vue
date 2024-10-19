<script setup>
import { ref, defineProps, watch } from "vue";

// get props from parent
const props = defineProps({
  vendingItems: Array,
});

// values for keys, bills base on ph peso, and vending machine items
const keys = [1, 2, 3, 4, 5, 6, 7, 8, 9, "*", 0, "Del"];
const pesoBills = [1000, 500, 100, 50, 20, 10, 5, 1];
const vendingNewArr = ref([...props.vendingItems]);

// values for items on the vending machine
// can be put on an obj or array but for now it will be declared as such
const itemNumber = ref(0);
const isOnItemList = ref(true);
const isCredentialsIncomplete = ref(true);
const isInsufficientBal = ref(true);

// values to be computed
const bill = ref(0);
const owedBill = ref(0);
const changeBill = ref("");

// Reset our values
const reset = () => {
  bill.value = 0;
  owedBill.value = 0;
  changeBill.value = "";

  itemNumber.value = 0;
  isOnItemList.value = true;
  isCredentialsIncomplete.value = true;
  isInsufficientBal.value = true;
};

// keyboard onClick actions function
const keyAction = (item) => {
  if (item === "*") reset();

  if (item === "Del") {
    let condition = String(itemNumber.value).length > 1;
    let newNum = itemNumber.value.toString().slice(0, -1);

    condition ? (itemNumber.value = parseInt(newNum)) : (itemNumber.value = 0);
  }

  const newItemNum = parseInt((itemNumber.value += item.toString()));

  return (itemNumber.value = newItemNum);
};

// add bills for payment function
const addBill = (item) => {
  const newbill = (bill.value += item);
  return (bill.value = newbill);
};

// minus bills for payment function
const minusBill = (item) => {
  if (item > bill.value) return;

  const newbill = (bill.value -= item);
  return (bill.value = newbill);
};

// compute change base on bill value function
const computeChange = () => {
  const changeArr = [];
  const isZeroBill = bill.value === 0;
  const isZeroOwed = owedBill.value === 0;
  let change = bill.value - owedBill.value;

  if (isZeroBill || isZeroOwed) return (isCredentialsIncomplete.value = false);

  if (bill.value < owedBill.value) return (isInsufficientBal.value = false);

  // loops peso bills to get the change by bill/coins
  pesoBills.forEach((item) => {
    const count = Math.floor(change / item);

    const computation = () => {
      let billOrCoins = item < 20 ? "coins" : "bills";
      changeArr.push(`${count} - ${item} ${billOrCoins}, `);
      change -= count * item;
    };

    count > 0 ? computation() : reset();
  });

  return (changeBill.value = changeArr.join("\n"));
};

// monitor the changes in input base on our keyboard/input field value
watch(itemNumber, (newValue) => {
  const findItem = vendingNewArr.value.find(
    (item) => item.itemNo == itemNumber.value
  );

  const setItemCondition = (condition) => {
    isOnItemList.value = condition;
  };

  if (findItem) {
    setItemCondition(true);

    isCredentialsIncomplete.value = true;
    isInsufficientBal.value = true;

    return (owedBill.value = findItem.itemPrice);
  }

  if (!findItem) {
    owedBill.value = 0;
    newValue === 0 ? setItemCondition(true) : setItemCondition(false);
  }
});
</script>

<!-- Display keyboard -->
<template>
  <div class="keyboardContainer">
    <!-- input field section to get itemNumber from-->
    <form @submit.prevent="computeChange">
      <input
        type="text"
        placeholder="input item number"
        @mousedown.prevent
        :value="itemNumber !== 0 ? itemNumber : ''"
      />
      <button>ok</button>
    </form>

    <!-- Monitor payment statuses[bills, owed, change] section-->
    <div class="payment">
      <div
        class="errPrompt"
        v-if="!isOnItemList || !isCredentialsIncomplete || !isInsufficientBal"
      >
        <span> X </span>
        {{
          !isOnItemList
            ? "Item not on the list"
            : !isCredentialsIncomplete
            ? "Please input item number then choose bill to pay"
            : !isInsufficientBal
            ? "Insufficient balance"
            : ""
        }}
      </div>
      <div>
        Payment: <span class="bill">Php {{ bill }}</span>
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

    <!-- keypad section -->
    <ul class="keypad">
      <li v-for="key in keys" :key="key">
        <div @click="keyAction(key)">
          <span>{{ key }}</span>
        </div>
      </li>
    </ul>

    <!-- add/minus/monitor bills section-->
    <h3 class="coinsTitle">
      Insert bill/coin: <span class="bill">Php {{ bill }}</span>
    </h3>
    <ul class="coins">
      <li v-for="peso in pesoBills" :key="peso" @click.stop="addBill(peso)">
        <div>
          <span>{{ peso }}</span>
          <div class="billCount" @click.stop="minusBill(peso)">
            <span>-</span>
          </div>
        </div>
      </li>
    </ul>
  </div>
</template>

<style scoped lang="scss">
$yellowish-bg-input: #be921a;
$reddish-color: #ff0037;
$pinkish-color: #e9b7ce;
$cement-color: #61817f;
$border-color: #80808070;
$greenish-color: #68ad00;

.keyboardContainer {
  padding: 2em 0;
  width: 100%;
  height: auto;
}

// =================== FORM =================== //
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
    border: 1px solid $yellowish-bg-input;
    font-size: 1.5em;
    width: 100%;
    padding: 0 2em;
    text-align: right;

    &:hover {
      outline: 3px solid $yellowish-bg-input;
    }

    &::placeholder {
      font-size: clamp(0.65em, 0.8vw, 0.8em);
      color: lighten($yellowish-bg-input, 25%);
    }
  }

  button {
    border: none;
    border-radius: 5px;
    box-shadow: -1px 1px 5px 1px lighten($border-color, 10%);
    width: 10em;
    cursor: pointer;
  }
}

// =================== PAYMENT =================== //
.payment {
  font-size: 0.85em;
  color: darken($cement-color, 20%);
  margin-bottom: 3em;

  .owedBill {
    font-weight: bold;
    font-size: 1.2em;
    color: $reddish-color;
  }

  .change {
    span {
      font-weight: 700;
      font-size: 1.2em;
      color: $cement-color;
    }
  }

  .errPrompt {
    margin: 0.7em 0;
    background: $pinkish-color;
    padding: 0.2em 1em;
    color: white;

    span {
      color: $reddish-color;
    }
  }
}

// =================== KEYPAD =================== //
.keypad {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 1em;
  padding: 3em 1em;
  border-radius: 5px;
  border: 1px solid $border-color;

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
      border: 1px solid $border-color;
      cursor: pointer;
    }
  }
}

// =================== COINS =================== //
.coinsTitle {
  margin: 3em 0 1em 0;
}

.coins {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 1em;

  li {
    all: unset;
    border: 1px solid $border-color;
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

// ====================================== //
// being called from different div elements so i set this aside for now
.bill {
  font-weight: bold;
  font-size: 1.2em;
  color: $greenish-color;
}
</style>
