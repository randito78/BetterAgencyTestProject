<script>

export default {
  data() {
    return {
      users: [],
      rows: [{id: 0, name: "", owner:""}],
      onStepOne: true,
    };
  },

  mounted() {
    this.fetchData();
  },

  methods: {
    addRow() {
      this.rows.push({name: "", owner:""});
    },

    deleteRow(i) {
      console.log(i);
      this.rows.splice(i, 1);
    },

    changeName(i, value) {
      this.rows[i].name = value.target.value;
    },

    changeAmount(i, value) {
      this.rows[i].value = value.target.value;
    },

    changeOwner(i, value) {
      this.rows[i].owner = value.target.value;
    },

    async fetchData() {
      const jsonResponse = await fetch('https://demo-api.bettercommissions.com/interview-data/users');
      if (jsonResponse.ok) {
        const actualResponse = await jsonResponse.json();
        this.users = actualResponse.users;
      }
    },
  },

  computed: {
    totalsPerOwner() {
      const totals = {};
      this.rows.map((row) => {
        if(!totals[row.owner]) {
          totals[row.owner] = row.amount;
        } else {
          totals[row.owner] += row.amount;
        }
      });

      return totals;
    },
  }
};
</script>

<template>
  <main class="main">
    <header class="header">Project</header>
    <div class="indicator">
      <div class="step">
        <div>
          <svg
            width="24"
            height="24"
            viewBox="0 0 24 24"
            fill="none"
            xmlns="http://www.w3.org/2000/svg"
          >
            <rect width="24" height="24" rx="12" fill="#1976D2" />
            <path
              d="M12.7715 7.42188V16H11.6875V8.77539L9.50195 9.57227V8.59375L12.6016 7.42188H12.7715Z"
              fill="white"
            />
          </svg>
        </div>
        <div class="indicator-text">Configuration</div>
      </div>
      <div class="connecting-line"/>
      <div class="step">
        <svg
          v-if="onStepOne"
          width="24"
          height="24"
          viewBox="0 0 24 24"
          fill="none"
          xmlns="http://www.w3.org/2000/svg"
        >
          <rect
            width="24"
            height="24"
            rx="12"
            fill="black"
            fill-opacity="0.38"
          />
          <path
            d="M14.7988 15.1094V16H9.21484V15.2207L12.0098 12.1094C12.3535 11.7266 12.6191 11.4023 12.8066 11.1367C12.998 10.8672 13.1309 10.627 13.2051 10.416C13.2832 10.2012 13.3223 9.98242 13.3223 9.75977C13.3223 9.47852 13.2637 9.22461 13.1465 8.99805C13.0332 8.76758 12.8652 8.58398 12.6426 8.44727C12.4199 8.31055 12.1504 8.24219 11.834 8.24219C11.4551 8.24219 11.1387 8.31641 10.8848 8.46484C10.6348 8.60938 10.4473 8.8125 10.3223 9.07422C10.1973 9.33594 10.1348 9.63672 10.1348 9.97656H9.05078C9.05078 9.49609 9.15625 9.05664 9.36719 8.6582C9.57812 8.25977 9.89062 7.94336 10.3047 7.70898C10.7188 7.4707 11.2285 7.35156 11.834 7.35156C12.373 7.35156 12.834 7.44727 13.2168 7.63867C13.5996 7.82617 13.8926 8.0918 14.0957 8.43555C14.3027 8.77539 14.4062 9.17383 14.4062 9.63086C14.4062 9.88086 14.3633 10.1348 14.2773 10.3926C14.1953 10.6465 14.0801 10.9004 13.9316 11.1543C13.7871 11.4082 13.6172 11.6582 13.4219 11.9043C13.2305 12.1504 13.0254 12.3926 12.8066 12.6309L10.5215 15.1094H14.7988Z"
            fill="white"
          />
        </svg><svg v-else width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
<rect width="24" height="24" rx="12" fill="#1976D2"/>
<path d="M14.7988 15.1094V16H9.21484V15.2207L12.0098 12.1094C12.3535 11.7266 12.6191 11.4023 12.8066 11.1367C12.998 10.8672 13.1309 10.627 13.2051 10.416C13.2832 10.2012 13.3223 9.98242 13.3223 9.75977C13.3223 9.47852 13.2637 9.22461 13.1465 8.99805C13.0332 8.76758 12.8652 8.58398 12.6426 8.44727C12.4199 8.31055 12.1504 8.24219 11.834 8.24219C11.4551 8.24219 11.1387 8.31641 10.8848 8.46484C10.6348 8.60938 10.4473 8.8125 10.3223 9.07422C10.1973 9.33594 10.1348 9.63672 10.1348 9.97656H9.05078C9.05078 9.49609 9.15625 9.05664 9.36719 8.6582C9.57812 8.25977 9.89062 7.94336 10.3047 7.70898C10.7188 7.4707 11.2285 7.35156 11.834 7.35156C12.373 7.35156 12.834 7.44727 13.2168 7.63867C13.5996 7.82617 13.8926 8.0918 14.0957 8.43555C14.3027 8.77539 14.4062 9.17383 14.4062 9.63086C14.4062 9.88086 14.3633 10.1348 14.2773 10.3926C14.1953 10.6465 14.0801 10.9004 13.9316 11.1543C13.7871 11.4082 13.6172 11.6582 13.4219 11.9043C13.2305 12.1504 13.0254 12.3926 12.8066 12.6309L10.5215 15.1094H14.7988Z" fill="white"/>
</svg>
        <div class="indicator-text">Summary</div>
      </div>
    </div>

    <table v-if="onStepOne" class="my-table">
      <tr class="header-row">
        <th class="row-header">Add plan name</th>
        <th class="row-header">$ Amount</th>
        <th class="row-header">Job Owner</th>
        <th class="row-header" />
      </tr>
      <tr class="table-row" v-for="(row, i) in rows" :key="i">
        <td class="row-header">
          <input
            v-model="rows[i].name"
            class="input-field"
            placeholder="Product name"
          />
        </td>
        <td class="row-header">
          <input
            type="number"
            v-model="rows[i].amount"
            class="input-field"
            placeholder="Dollar amount"
          />
        </td>

        <td class="row-header">
          <select
            class="input-field owner-select"
            v-model="rows[i].owner"
            placeholder="Select job owner"
          >
            <option disabled value="">Select job owner</option>
            <option v-for="user in users" :key="user.name">
              {{ user.name }}
            </option>
          </select>
        </td>

        <td class="row-header my-svg">
          <svg
            class="trashcan"
            @click="() => deleteRow(i)"
            width="14"
            height="18"
            viewBox="0 0 14 18"
            fill="none"
            xmlns="http://www.w3.org/2000/svg"
          >
            <path
              d="M1 16C1 17.1 1.9 18 3 18H11C12.1 18 13 17.1 13 16V4H1V16ZM14 1H10.5L9.5 0H4.5L3.5 1H0V3H14V1Z"
              fill="#3A3541"
              fill-opacity="0.54"
            />
          </svg>
        </td>
      </tr>
    </table>
    <table v-else class="my-table">
      <tr class="header-row">
        <th class="row-header">$ Sum</th>
        <th class="row-header">Job Owner</th>
      </tr>
      <tr
        class="table-row"
        v-for="(row, i) in Object.keys(totalsPerOwner)"
        :key="i"
      >
        <td class="row-header">
          {{ totalsPerOwner[row] }}
        </td>
        <td class="row-header">
          {{ row }}
        </td>
      </tr>
    </table>

    <div v-if="onStepOne" class="buttons">
      <div class="left-button" @click="addRow">+ add row</div>
      <div class="right-button" @click="onStepOne = false">next</div>
    </div><div v-else class="buttons">
      <div class="left-button" @click="onStepOne = true">{{"< back"}}</div>
    </div>
  </main>
</template>

<style scoped>
  .indicator {
    padding: 24px;
    display: flex;
    /* justify-content: space-between; */
    margin-bottom: 48px;
    background: #FFFFFF;
    box-shadow: 0px 3px 1px -2px rgba(0, 0, 0, 0.2), 0px 2px 2px rgba(0, 0, 0, 0.14), 0px 1px 5px rgba(0, 0, 0, 0.12);
  }

  .connecting-line {
    border-bottom: 1px solid rgba(0, 0, 0, 0.12);
    width: 740px;
    margin: 8px;
    margin-bottom: 14px;
  }

  .header-row {
    border-bottom: 1px solid rgba(0, 0, 0, 0.12);
  }

  .trashcan {
    cursor: pointer;
  }

  .table-row {
    border-bottom: 1px solid rgba(0, 0, 0, 0.12);
  }

  .my-svg {
    padding-left: 17px;
    padding-right: 17px;
  }

  .main {
    width: 1033px;
    margin: auto;
    text-align: center;
    /* width: 1033px; */
  }

  .table-headers {
    display: flex;
  }

  .owner-select {
    /* color: rgba(0, 0, 0, 0.87); */
    cursor: pointer;
  }

  .step {
    display: flex;
  }

  table > th {
    text-align: left;
}

.indicator-text {
  margin-top: 3px;
  margin-left: 8px;
}

.my-table {
  border-collapse: collapse;
  border-spacing: 16px;
  text-align: left;
  width: 100%;
}

.input-field {
  box-sizing: border-box;

  /* Auto layout */
  display: flex;
  flex-direction: row;
  align-items: center;
  padding: 8px 12px;
  gap: 10px;

  width: 234px;
  height: 40px;

  /* Light/Background/Paper */

  background: #FFFFFF;
  /* black/0.42 */

  border: 1px solid rgba(0, 0, 0, 0.42);
  border-radius: 4px;

  /* Inside auto layout */

  flex: none;
  align-self: stretch;
  flex-grow: 0;
  margin-right: 90px;
}

.buttons {
  display: flex;
  justify-content: space-between;
}

.row-header {
  padding-top: 16px;
  padding-bottom: 16px;
  padding-left: 10px;
  color: rgba(0, 0, 0, 0.87);
}

.left-button {
  cursor: pointer;
/* v-text/button */

font-family: 'Roboto';
font-style: normal;
font-weight: 500;
font-size: 14px;
line-height: 36px;
/* identical to box height, or 257% */

display: flex;
align-items: center;
text-align: center;
letter-spacing: 1.25px;
text-transform: uppercase;

/* custom/primary */

color: #1976D2;


/* Inside auto layout */

flex: none;
flex-grow: 0;
}

.right-button {
  cursor: pointer;
  display: flex;
flex-direction: row;
align-items: center;
padding: 0px 16px;
gap: 16px;

font-family: 'Roboto';
font-style: normal;
font-weight: 500;
font-size: 14px;
line-height: 36px;
/* identical to box height, or 257% */

display: flex;
align-items: center;
text-align: center;
letter-spacing: 1.25px;
text-transform: uppercase;

/* shades/white */

color: #FFFFFF;

/* custom/primary */

background: #1976D2;
color: white;
border-radius: 36px;
}

.header {
  /* Project */
margin-top: 48px;
width: 77px;
height: 32px;
left: 0px;
top: 0px;

margin-bottom: 24px;

/* Light/Header/Header L */
font-family: 'Roboto';
font-style: normal;
font-weight: 600;
font-size: 24px;
line-height: 32px;
/* identical to box height, or 133% */

color: #000000;
}

.my-table {
  margin-bottom: 40px;
}
</style>
