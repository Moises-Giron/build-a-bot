<template>
    <div>
      <div class="top-row">
        <div class="top part">
          <img :src="selectedRobot.head.imageUrl" alt="head" />
          <button
            @click="selectPreviousHead()" class="prev-selector">&#9668;
          </button>
          <button
            @click="selectNextHead()" class="next-selector">&#9658;
          </button>
        </div>
      </div>
      <div class="middle-row">
        <div class="left part">
          <img :src="selectedRobot.leftArm.imageUrl" alt="left arm" />
          <button
            @click="selectPreviousLeftArm()" class="prev-selector">&#9650;
          </button>
          <button
            @click="selectNextLeftArm()" class="next-selector">&#9660;
          </button>
        </div>
        <div class="center part">
          <img :src="selectedRobot.torso.imageUrl" alt="torso" />
          <button
            @click="selectPreviousTorso()" class="prev-selector">&#9668;
          </button>
          <button
            @click="selectNextTorso()" class="next-selector">&#9658;
          </button>
        </div>
        <div class="right part">
          <img :src="selectedRobot.rightArm.imageUrl" alt="right arm" />
          <button
            @click="selectPreviousRightArm()" class="prev-selector">&#9650;
          </button>
          <button
            @click="selectNextRightArm()" class="next-selector">&#9660;
          </button>
        </div>
      </div>
      <div class="bottom-row">
        <div class="bottom part">
          <img :src="selectedRobot.base.imageUrl" alt="base" />
          <button
            @click="selectPreviousBase()" class="prev-selector">&#9668;
          </button>
          <button
            @click="selectNextBase()" class="next-selector">&#9658;
          </button>
        </div>
      </div>
    </div>
</template>
<script>
import parts from '../data/parts';

// Can create private helper functions - don't need to be part of component metadata object
//      since they are used internally
// Can't be called within template, but can be called within component's methods
function getNextValidIndex(index, length) {
  const incrementedIndex = index + 1;
  return incrementedIndex > length - 1 ? 0 : incrementedIndex;
}

function getPreviousValidIndex(index, length) {
  const deprecatedIndex = index - 1;
  return deprecatedIndex < 0 ? length - 1 : deprecatedIndex;
}

export default {
  name: 'RobotBuilder',
  data() {
    return {
      availableParts: parts,
      selectedHeadIndex: 0,
      selectedRightArmIndex: 0,
      selectedTorsoIndex: 0,
      selectedLeftArmIndex: 0,
      selectedBaseIndex: 0,
    };
  },
  computed: {
    selectedRobot() {
      return {
        head: this.availableParts.heads[this.selectedHeadIndex],
        leftArm: this.availableParts.arms[this.selectedLeftArmIndex],
        torso: this.availableParts.torsos[this.selectedTorsoIndex],
        rightArm: this.availableParts.arms[this.selectedRightArmIndex],
        base: this.availableParts.bases[this.selectedBaseIndex],
      };
    },
  },
  methods: {
    // selectNextHead() {
    //   if (this.selectedHeadIndex < this.availableParts.heads.length - 1) {
    //     this.selectedHeadIndex += 1;
    //   }
    // },
    // selectPreviousHead() {
    //   if (this.selectedHeadIndex > 0) {
    //     this.selectedHeadIndex -= 1;
    //   }
    // },
    selectNextHead() {
      this.selectedHeadIndex = getNextValidIndex(
        this.selectedHeadIndex,
        this.availableParts.heads.length,
      );
    },
    selectPreviousHead() {
      this.selectedHeadIndex = getPreviousValidIndex(
        this.selectedHeadIndex,
        this.availableParts.heads.length,
      );
    },
    selectNextRightArm() {
      this.selectedRightArmIndex = getNextValidIndex(
        this.selectedRightArmIndex,
        this.availableParts.arms.length,
      );
    },
    selectPreviousRightArm() {
      this.selectedRightArmIndex = getPreviousValidIndex(
        this.selectedRightArmIndex,
        this.availableParts.arms.length,
      );
    },
    selectNextTorso() {
      this.selectedTorsoIndex = getNextValidIndex(
        this.selectedTorsoIndex,
        this.availableParts.torsos.length,
      );
    },
    selectPreviousTorso() {
      this.selectedTorsoIndex = getPreviousValidIndex(
        this.selectedTorsoIndex,
        this.availableParts.torsos.length,
      );
    },
    selectNextLeftArm() {
      this.selectedLeftArmIndex = getNextValidIndex(
        this.selectedLeftArmIndex,
        this.availableParts.arms.length,
      );
    },
    selectPreviousLeftArm() {
      this.selectedLeftArmIndex = getPreviousValidIndex(
        this.selectedLeftArmIndex,
        this.availableParts.arms.length,
      );
    },
    selectNextBase() {
      this.selectedBaseIndex = getNextValidIndex(
        this.selectedBaseIndex,
        this.availableParts.bases.length,
      );
    },
    selectPreviousBase() {
      this.selectedBaseIndex = getPreviousValidIndex(
        this.selectedBaseIndex,
        this.availableParts.bases.length,
      );
    },
  },
};
</script>
<style>
    .part {
      position: relative;
      width: 200px;
      height: 200px;
      border: 3px solid #aaa;
    }

    .part img {
      width: 200px;
    }

    .top-row {
      display: flex;
      justify-content: space-around;
    }

    .middle-row {
      display: flex;
      justify-content: center;
    }

    .bottom-row {
      display: flex;
      justify-content: space-around;
      border-top: none;
    }

    .top {
      border-bottom: none;
    }

    .left {
      border-right: none;
    }

    .right {
      border-left: none;
    }

    .left img {
      transform: rotate(-90deg);
    }

    .right img {
      transform: rotate(90deg);
    }

    .bottom {
      border-top: none;
    }

    .prev-selector {
      position: absolute;
      z-index: 1;
      top: -3px;
      left: -28px;
      width: 25px;
      height: 206px;
    }

    .next-selector {
      position: absolute;
      z-index: 1;
      top: -3px;
      right: -28px;
      width: 25px;
      height: 206px;
    }

    .center .prev-selector,
    .center .next-selector {
      opacity: 0.8;
    }

    .left .prev-selector {
      top: -28px;
      left: -3px;
      width: 179px;
      height: 25px;
    }

    .left .next-selector {
      top: auto;
      bottom: -28px;
      left: -3px;
      width: 179px;
      height: 25px;
    }

    .right .prev-selector {
      top: -28px;
      left: 24px;
      width: 179px;
      height: 25px;
    }

    .right .next-selector {
      top: auto;
      bottom: -28px;
      left: 24px;
      width: 179px;
      height: 25px;
    }

    .right .next-selector {
      right: -3px;
    }
</style>
