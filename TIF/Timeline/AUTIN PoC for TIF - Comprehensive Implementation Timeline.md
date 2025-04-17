# AUTIN PoC for TIF - Comprehensive Implementation Timeline

## Phase 1 Detailed Implementation Timeline: Alarm Compression & Correlation

```mermaid
gantt
    title AUTIN Phase 1: Alarm Suppression & Correlation Implementation
    dateFormat  YYYY-MM-DD
    axisFormat  %d-%b
    todayMarker on

    section Goal & Preparation
    AUTIN Capability Demonstration Planning      :active, prep1, 2025-04-17, 3d
    Huawei EMS Alarm Data Preparation (DWDM, IP, Access) :active, prep2, 2025-04-20, 3d
    Huawei Syslog Preparation for Metro and PE   :active, prep3, 2025-04-20, 3d
    Documentation Processing (Parallel)          :doc, 2025-04-17, 30d

    section Alarm Suppression Implementation
    Integrate Huawei EMS Alarm Data              :crit, imp1, after prep2, 3d
    Set Up Correlation Engine with Huawei Rules  :crit, imp2, after imp1, 3d
    Test Alarm Suppression Capabilities          :crit, imp3, after imp2, 3d
    Evaluate Results without Inventory/Topology  :crit, imp4, after imp3, 2d

    section Expected Results Validation
    Test AUTIN iFM Module for Alarm Reduction    :val1, after imp3, 3d
    Validate Correlation Rules Effectiveness     :val2, after imp4, 3d
    Measure Compression Efficiency               :val3, after val2, 2d
    Resource Efficiency Documentation            :val4, after val3, 2d

    section Sumbagsel Use Case Demonstration
    Sumbagsel Scenario Configuration             :sum1, after imp4, 3d
    Fiber Cut Scenario Simulation                :sum2, after sum1, 2d
    Multiple IP Alarms Correlation Demo          :sum3, after sum2, 2d
    Auto-Close Functionality Demonstration       :sum4, after sum3, 2d
    
    section Stakeholder Engagement
    Results Compilation and Analysis             :eng1, after val4, 3d
    Capability Showcase Preparation              :eng2, after eng1, 2d
    TIF Stakeholder Presentation                 :milestone, pres, after eng2, 0d
    ROI and Resource Saving Discussion           :eng3, after pres, 2d
    
    section Evaluation & Decision
    Capability Assessment Meeting                :crit, eval, after eng3, 1d
    Implementation Decision for Phase 1          :crit, milestone, decision, after eval, 0d
```

### Journey Plan:

1. **Goal Integration**:
   - Explicitly focuses on testing "alarm suppression in iFM module using Huawei EMS alarm data only" as stated in the journey plan

2. **Data Sources Specified**:
   - Includes the exact data sources mentioned in the pre-requisites:
     - "Huawei EMS data from DWDM, IP, Access"
     - "Syslog data for Metro and PE"

3. **Key Actions Incorporated**:
   - Added specific tasks that match the key actions in the journey plan:
     - "Integrate Huawei EMS alarm data (DWDM, IP, Access)"
     - "Set up correlation engine using Huawei's rules"
     - "Test alarm suppression capabilities"
     - "Evaluate results without inventory or topology data"

4. **Expected Results Validation**:
   - Includes tasks to validate all the expected results in the journey plan:
     - "Test AUTIN iFM module for alarm reduction"
     - "Validate correlation rules from Huawei's experience"
     - "Evaluate alarm suppression effectiveness"

5. **Sumbagsel Focus**:
   - Added a dedicated section for Sumbagsel case demonstration based on the concern raised in the MoM about the need to show capability with Sumbagsel-specific cases

This timeline now perfectly aligns with the journey plan while maintaining a practical implementation approach that doesn't require TIF data or wait for Nodin approval. It demonstrates how we can achieve the goals outlined in Chapter 1 using only Huawei's data and expertise.
