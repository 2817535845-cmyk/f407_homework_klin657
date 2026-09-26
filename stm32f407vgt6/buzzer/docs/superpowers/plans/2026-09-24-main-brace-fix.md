# Main Brace Fix Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Restore compilation by closing the `main()` function after the TIM9 breathing-loop block.

**Architecture:** No behavior changes are needed. The current source closes the dimming loop and the infinite loop but leaves `main()` open, which causes the compiler to parse subsequent function definitions inside `main()`.

**Tech Stack:** C11, STM32 HAL, CMake/Ninja, GNU Arm Embedded Toolchain.

---

### Task 1: Close `main()` and verify the Debug build

**Files:**
- Modify: `Core/Src/main.c:124-128`
- Test: CMake Debug build

- [ ] **Step 1: Use the existing failing compile as the regression test**

Run:

```bash
cmake --build --preset Debug
```

Expected before the fix: failure containing `expected declaration or statement at end of input`.

- [ ] **Step 2: Add the missing closing brace**

Change the end of the main loop to:

```c
        }
    }
}

/**
```

The first brace closes the dimming `for`, the second closes `while (1)`, and the third closes `main()`.

- [ ] **Step 3: Build the Debug preset again**

Run:

```bash
cmake --build --preset Debug
```

Expected: exit status 0 and a linked `board.elf` artifact.
