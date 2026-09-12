# UE 5.7.4 UMG Carousel Component Test

**Candidate Name:** Carlos Zavala  
**Submission Date:** September 11, 2026  
**Target Engine Version:** Unreal Engine 5.7.4 (Blueprint Only)  

---

## 1. Overview & Architecture

This project implements a data-driven mission-select carousel component in UMG (`WBP_Carousel`). The architecture decouples data parsing, dynamic layout generation, and gamepad navigation.

### Key Design & Architecture Choices
* **Data-Driven Dynamic Spawning:** Built programmatically from `DT_CarouselItems` at runtime. Items are dynamically instantiated (`WBP_CarouselCard`) and populated via struct data during `Construct` rather than manually placed in the designer.

* **Core Priority Focus:** Due to time constraints, core architecture, dynamic spawning, and controller-first navigation were prioritized to establish a solid foundation.

---

## 2. Navigation & Boundary Choices

### Selected Approach: [Clamped Ends OR Wrap-Around]
* **Implementation:** I implemented clamped boundary limits using `Clamp (Integer)` on `TargetFocusIndex` within `WBP_Carousel`. 

* **Rationale:** Clamping gives a strong sense of boundaries to list items, providing clear visual feedback when reaching the edge of the dataset.

---

## 3. Motion, Animation & Layout Specs

* **Scroll View Target Focusing:** To protect core functionality within the allotted timebox, the custom mathematical spatial offset functions (manual render translation/opacity scaling math) were replaced with a built-in feature of the Scroll View component to scroll into view and focus the current target index element.

* **Navigation Behavior:** Updating `TargetFocusIndex` triggers the Scroll View's native focus/scroll logic, smoothly centering the active target widget without needing complex custom coordinate math.

* **Toggle Show/Hide Motion:** The `ToggleCarousel` action (Q key) smoothly animates container visibility/transform.

---

## 4. Input & Controller Implementation

* **Gamepad / Keyboard Navigation:** Bound using the supplied Enhanced Input Actions (WASD / D-Pad / Thumbstick).

* **Debounce Logic:** Integrated input cooldown/debounce logic to ensure smooth, controlled single steps per press/hold across D-pad and analog stick inputs.

* **Focus Visibility:** Clear visual differentiation maintained for the focused card index.

---

## 5. AI Tool Disclosure

In accordance with test instructions:

* **Tools Used:** Unreal Engine 5, Blueprints, Git, Gemini
* **Approximate Time/Usage:** 8.5 hrs
* **Scope of Use:** UMG components, focus settings, project progress and tracking, Blueprints logic.

---

## 6. Self-Direction & Next Steps (Unreached Goals)

To protect Core stability within the timebox, development paused after Phase 3.1 (Gamepad & Scroll View Focus Navigation). Given additional time, the remaining features would be implemented in this order:

1. **Custom Spatial Transform Math:** Re-implement custom mathematical functions (dynamic scale, opacity, and depth offsets per card based on distance from index) to replace the standard Scroll View focusing.

2. **Mouse Input Setup (Phase 3.2):** Implement hover feedback on `WBP_CarouselCard`, off-center click-to-focus routing, and click-on-focused item selection.

3. **Slate Focus Navigation Override (Phase 3.3):** Override `OnKeyDown` / Slate focus rules to handle native arrow key Slate focus collision explicitly.

4. **Selection Dispatcher (Phase 4):** Complete the `OnCarouselItemSelected` Event Dispatcher to broadcast selection events to consuming screens.

5. **Item Pooling & Recycling (Extended):** Convert layout generation to an active widget pool (5–7 cards) for handling large datasets (200+ items).

---

## 7. Submission Checklist Verification

* [x] **Project Zip:** Cleaned (`Binaries`, `Intermediate`, `Saved`, and `DerivedDataCache` folders deleted).

* [x] **Video:** 45–60 second unbroken video demonstrating gamepad navigation, show/hide, and rapid stress-test inputs.

        https://youtu.be/uakEYarEe64

* [x] **README:** Complete documentation of choices, timing, and AI disclosure.
