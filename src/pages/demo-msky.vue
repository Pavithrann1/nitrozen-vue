<template>
  <div id="app">
    <div class="main-div">
      <div class="title">Radio</div>
      <div class="main-div space-between">
        <nitrozen-radio
          :name="'radio-1'"
          v-model="radioModel"
          @change="changeEvent"
          :radioValue="'1'"
          >Basic Radio 1</nitrozen-radio
        >
        <nitrozen-radio
          :name="'radio-1'"
          v-model="radioModel"
          @change="changeEvent"
          :radioValue="'2'"
          >Basic Radio 2</nitrozen-radio
        >
        <nitrozen-radio
          :name="'radio-1'"
          v-model="radioModel"
          @change="changeEvent"
          :radioValue="'3'"
          >Basic Radio 3</nitrozen-radio
        >
        <!-- {{ radioModel }} -->
      </div>
      <div class="break"></div>
      <div class="title">Check Box</div>
      <div class="main-div space-between">
        <nitrozen-checkbox v-model="singleCheckboxModel"
          >Test Single Checkbox</nitrozen-checkbox
        >
        <span>Checkbox model value: {{ singleCheckboxModel }}</span>
      </div>

      <div class="main-div space-between">
        <nitrozen-checkbox
          v-model="checkArray" id="a" name="a"
          @change="testFunc($event)"
          checkboxValue="Check 1"
          >Check 1</nitrozen-checkbox
        >
        <nitrozen-checkbox
          checkboxValue="Check 2" id="b" name="b"
          @change="testFunc($event)"
          v-model="checkArray"
          >Check 2</nitrozen-checkbox
        >
        <nitrozen-checkbox
          checkboxValue="Check 3" id="c" name="c"
          @change="testFunc($event)"
          v-model="checkArray"
          >Check 3</nitrozen-checkbox
        >
        <nitrozen-checkbox
          checkboxValue="Check 4" id="d" name="d"
          @change="testFunc($event)"
          v-model="checkArray"
          >Check 4</nitrozen-checkbox
        >
        <!-- <span>Checked names: {{ checkArray }}</span> -->

        <nitrozen-checkbox :disabled="true" v-model="abcd"
          >Checkbox</nitrozen-checkbox
        >
        {{ abcd }}
      </div>


    </div>

    </div> 
   
</template>

<script>
import { countries } from "./countries";
import {NitrozenRadio,NitrozenCheckBox,NitrozenButton} from "../components";
export default {
  name: "App",
  components : {
NitrozenRadio,"nitrozen-checkbox":NitrozenCheckBox,"nitrozen-toggle-btn":NitrozenButton
  },
  data() {
    return {

      tabArray: ["Item1", "Item2", "Item3"],
      multiSelect: [11,12,13,14,15,21,22,23,24,25],
      numberOfClick: 0,
      abcd: true,
      isActive: false,
      singleCheckboxModel: true,
    
      checkArray: ["Check 1"],
      radioModel: "1",
    
      autofocusSearch: false,
      linkTitle: 'External Link',
      externalLink: 'https://www.example.com', // Replace with your desired external link
      linkText: 'Click me to open in a new tab!',
      routerLinkTitle: 'Internal Link',
      routerLinkText: 'Click me for an internal link!',
      linkAppearance: 'body-md', // Replace with your desired text appearance class
      routerProvider: {
        to: '/some-internal-route', // Replace with the internal route you want to navigate to
      },



      isPanelOpen: false,
      sheetContent: [
        "Dynamic Content 1",
        "Dynamic Content 2",
      ],
      stepperConfig: {
        activeStep: 0,
        onBack: this.onBackMethod, 
        totalStep: 2
      }
    };
  },
  mounted() {
    this.dropdownItemsFiltered = this.dropdownItemsGroup;
    // setTimeout(() => {
    //   this.autofocusSearch = true;
    // }, 5000);
  },
  methods: {
    stepperNext() {
      let next = this.stepper.activeIndex + 1;
      if (this.stepper.maxActiveIndex < next) {
        this.stepper = Object.assign({}, this.stepper, {
          maxActiveIndex: next,
        });
      }
      this.stepper = Object.assign({}, this.stepper, { activeIndex: next });
    },
    stepperClicked(event) {
      this.stepper = Object.assign({}, this.stepper, {
        activeIndex: event.nextIndex,
      });
    },
    someFunc() {
      this.numberOfClick += 1;
    },
    addOption(value) {
      console.log(value);
    },
    testFunc(event) {
      console.log(event);
    },

    checkValue(event) {
      console.log(event);
      this.abcd = event.target.checked;
    },
    addFruit(event) {
      var value = this.fruitName;
      let obj = {
        name: value,
      };
      this.fruits.push(obj);
      this.fruitName = "";
    },
    removeFruit(index) {
      this.fruits.splice(index, 1);
    },
    setSelectItems: function(item) {
      let index = this.selectedItems.indexOf(item);
      if (index == -1) {
        this.selectedItems.push(item);
      } else {
        this.selectedItems.splice(index, 1);
      }
    },
    changeEvent: function(event) {
      console.log(event, "event");
    },
    openDialog(type) {
      switch (type) {
        case "alert":
          this.$refs["alert_dialog"].open({ width: "300px" });
          break;
        case "confirm":
          this.$refs["confirm_dialog"].open({
            width: "500px",
            positiveButtonLabel: "Delete",
            negativeButtonLabel: "Cancel",
            neutralButtonLabel: false,
          });
          break;
        case "choose":
          this.$refs["choose_dialog"].open({ width: "300px", height: "400px" });
          break;
        default:
          this.$refs["alert_dialog"].open({ dismissible: false });
      }
    },
    onCloseDialog(data) {
      window.console.log(data);
    },
    paginationChange(e) {
      console.log(e);
    },
    dropdownInputChange(e) {
      console.log(e);
      if (e && e.text) {
        let text = e.text;
        this.dropdownItemsFiltered = this.dropdownItemsGroup.filter(
          (a) =>
            a.text.toLowerCase().indexOf(text.toLowerCase()) > -1 ||
            a.isGroupLabel
        );
        this.dropdownItemsFiltered = this.dropdownItemsFiltered.filter(
          (a, i, arr) => {
            if (a.isGroupLabel) {
              if (arr[i + 1] && !arr[i + 1].isGroupLabel) {
                return true;
              }
              return false;
            }
            return true;
          }
        );
      } else {
        this.dropdownItemsFiltered = this.dropdownItemsGroup;
      }
    },
    tabChange(event) {
      console.log(event);
    },
    handleImageLoad(event) {
      // Handle image load event
      console.log("Image Loding....")
    },
    handleImageError(event) {
      // Handle image error event
      console.log("Image handle Error....");
    },
    handleImageClick(event) {
      // Handle image click event
      console.log("Image Click.....");
    },
    showToastNotification() {
      this.showToast = true;
    },
    showNudgeNotification() {
      this.showNudge = true;
    },
    onCloseToast() {
      this.showToast = false;
    },
    onCloseNudge() {
      this.showNudge = false;
    },
    onClickPrimary() {
      console.log('Primary button clicked.');
    },
    onClickSecondary() {
      console.log('Secondary button clicked.');
    },
    showPanel() {
      this.isPanelOpen = true; 
    },
    closePanel() {
      this.isPanelOpen = false;
    },
    openBottomSheet() {
      if (this.$refs.bottomSheet) {
        this.$refs.bottomSheet.open(); // Call the open method
      }
    },
    openBottomSheetStepper() {
      if (this.$refs.bottomSheetStepper) {
        this.$refs.bottomSheetStepper.open(); // Call the open method
      }
    },
    handleHeaderPrefixClick() {
      // Handle the header prefix click event here
    },
    onBackMethod() {
      if (this.stepperConfig.activeStep > 0) {
        this.stepperConfig.activeStep--;
      }
    }
  },
};
</script>

<style lang="less">
@import '../base/mixin.less';

body {
  font-family: "Inter";
  .color-palette(jiomart);
}
.main-div {
  margin-top: 2%;
  padding: 40px;
  background: #f8f8f8;
  &.pad {
    padding: 24px;
  }
  &.bg-white {
    background: #ffffff;
  }
  .title {
    font-size: 24px;
    font-family: Arial, Helvetica, sans-serif;
    font-weight: 700;
    text-align: center;
  }
  .break {
    background: #ffffff;
    width: 100%;
    height: 8px;
    margin-bottom: 18px;
  }
}

.space-between {
  display: flex;
  justify-content: space-evenly;
  flex-wrap: wrap;
  .box {
    margin: 20px;
  }
}


.n-radio-group input[type='radio']:checked + label:before {
    border: 1px solid #0078ad;
    box-shadow: inset 0 0 0 0.375em #0078ad;
}
.n-radio-group input[type='radio']:checked + label:hover:before {
    border: 1px solid #0078ad;
    box-shadow: inset 0 0 0 0.375em #0078ad;
}
.n-checkbox-container input:checked ~ .n-checkbox {
    border-color: #0078ad;
    background-color: #0078ad;
}

.n-checkbox-container input:checked ~ .n-checkbox:hover {
    background-color: #0078ad;
}
.n-checkbox-container {
    color: rgba(0,0,0,.65);
}

</style>
