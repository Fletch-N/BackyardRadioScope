# **Adaptive Stacking for Long-Exposure Sky Imaging**
## **Overview**
This research explores real-time FPGA-driven sky imaging, tracking Earth's rotation to accumulate long-exposure data while maintaining a **fixed final storage size** per image.

## **1. High-Speed Sky Resolution via FPGA**
- **Sky image resolution:** 7200 × 7200 (arcminute precision)
- **Single full-sky scan time:** ~3.6 milliseconds
- **Earth rotation rate:** 15° per hour (0.25 arcminutes/sec)
- **Tracking integration window:** Adjusting in steps of 0.25 arcminutes per second

## **2. Stacking Over Time to Simulate Long Exposure**
Instead of storing multiple images separately:
✅ **Signal accumulation for enhanced sensitivity**  
✅ **Noise reduction via coherent phase alignment**  
✅ **Final storage remains constant (~208 MiB per full-sky image)**  

### **Exposure Duration & Data Integration**
- **Long-exposure accumulation window:** Hours or days
- **Pixel integration weighting:** Brighter sources converge faster, weaker signals accumulate gradually
- **Data overwrite model:** Progressive averaging replaces transient noise without exceeding storage limits

## **3. Synchronization Strategies**
### **FPGA-Based Time Synchronization**
- **Atomic/GPS-clocked FPGA timing ensures microsecond precision**
- **Nanosecond-phase coherence eliminates drift errors**
- **Beam positions are dynamically corrected before stacking integration**

### **Earth Rotation Correction & Adaptive Stacking**
- **Each sky section shifts ~0.25 arcminutes per second**
- **Tracking algorithms adjust pixel alignment dynamically before each frame is accumulated**
- **Multi-pass coherence correction prevents rotational blur**

### **Doppler & Phase Drift Compensation**
- **Real-time phase delay algorithms adjust incoming signals dynamically**
- **GPU-assisted Fourier-domain stacking ensures long-term alignment**
- **Interferometric calibration markers maintain continuous phase-lock**

### **Precision Timekeeping & Network Synchronization**
- **GPS-disciplined atomic clocks ensure absolute synchronization**
- **Precision Time Protocol (PTP) used for FPGA/GPU time coherence**
- **Multi-node distributed timing correction guarantees pixel-level precision across stacking cycles**

## **4. Horizon Shift Considerations & Tracking Optimization**
Since Earth rotates **15° per hour**, parts of the **120° sky view** will eventually **drift below the horizon**.

### **Strategies for Continuous Coverage**
✅ **Dynamic field realignment** – Adjust tracking window every few minutes  
✅ **Multi-antenna spatial overlap** – Deploy redundant phased array sectors for uninterrupted sky mapping  
✅ **Time-based signal weighting** – Prioritize sections with prolonged exposure, minimizing loss  
✅ **Sky rotation predictive stacking** – Pre-adjust pixel alignment based on Earth rotation models  

## **5. Next Steps**
- **Refine FPGA phase coherence algorithms for long-exposure tracking**
- **Implement GPU-enhanced Fourier stacking methods for noise rejection**
- **Optimize parallel storage for adaptive overwriting without expansion**