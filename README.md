# 🫀 Imaging Examination of the Heart (Updated: 2026-09-18)

Echocardiography model (draft, updated 2026-09-18)
<img width="1446" height="1127" alt="image" src="https://github.com/user-attachments/assets/03bdd87d-9626-4f7b-8b94-b2c8cd38d4cb" />


MRI model (predraft)
<img width="1269" height="788" alt="image" src="https://github.com/user-attachments/assets/b3f4059f-d4b8-40d4-8734-bfff24b61675" />


## Body Structure
The structures that are measured are the larger ones such as the left and right ventricles, left and right atria, but also other parts like the aorta, aortic valve, among others. Specific parts of certain structures are also measured, for example, Left ventricle posterior wall.  

At the Physiological Clinic, there is no standard procedure for how an examination is conducted; it varies between different BMAs. During analysis and report writing, however, one usually works with one structure at a time.

Body structure can be handled in different ways, either as a part of the element for the measurement value or on the level of the archetype, or on an specific element for structure/laterality in the archetype.

At present, the anatomical structure concerned is described in the name of each measurement value element. If there is a need to specify it explicitly, the Structured body site slot could be used together with the cluster archetype openEHR-EHR-CLUSTER.anatomical_location.v1.

## Laterality
The number of parameters listed by the Physiological Clinic differs significantly between the right and left ventricles. This is due to several reasons: historically, the left ventricle was considered more important than the right ventricle and therefore received more focus. But nowadays, the thinking is somewhat different. Furthermore, the right ventricle has a special shape, like a pyramid with a "banana-shaped" base. This means that Simpson's method cannot be used as it assumes a more "bullet-shaped" form. It is simply easier to perform calculations on the left ventricle.  
This circumstance is unique to echocardiography; when it comes to MRI, volumes can be calculated in the same way for both ventricles.

Laterality can be handled in different ways, either as a part of the element for the measurement value or on a specific element for structure/laterality.

At present, the anatomical structure concerned is described in the name of each measurement value element. If there is a need to specify it explicitly, the Structured body site slot could be used together with the cluster archetype openEHR-EHR-CLUSTER.anatomical_location.v1.

**openEHR**: body structure + physical quantity will be handled under `Items` in the cluster archetype.

## Mode
Describes the technique used to produce the image.

**openEHR**: Since this describes a circumstance around the measurement, it should be expressed under `Protocol` in the observation archetype.

**SNOMED CT**: selection of modes: https://browser.ihtsdotools.org/?perspective=full&conceptId1=278292003&edition=MAIN/SNOMEDCT-SE/2025-05-31&release=&languages=sv,en

- **M-mode**  
  Motion-mode, a graph that shows a one-dimensional line representing the heart's movement and structure over time. Mainly used for diameter, thickness, and distance.

- **2D**  
  A two-dimensional image with width and depth relative to the probe.

  In addition to viewing one plane of the heart, multiple views (Views) can be used to calculate volumes or ejection fractions.

  **Single plane**: Measurement is based on one view.

  **Biplane**: Measurement is based on two views.

  **Triplane**: Measurement is based on three views.

- **3D**  
  Measurement is based on a three-dimensional image. The advantage is that the image is not based on the assumptions required for biplane or triplane.

- **Doppler**  
  A two-dimensional image supplemented with a color-coded layer representing blood flows (Spectral Doppler (Continuous wave doppler and Pulsed wave doppler) and tissue velocities (Tissue Doppler) based on frequency changes.

- **Speckle tracking**  
  [text]

## View
Views or projections, i.e., different angles from which the heart can be seen.

**openEHR**: Since this describes a circumstance around the measurement, it should be expressed under `Protocol` in the observation archetype. Our suggestion is that this should be included in a new archetype describing the technique of image analysis/ultrasound/echocardiographic measurement.

**SNOMED CT**: selection of views: https://browser.ihtsdotools.org/?perspective=full&conceptId1=399043000&edition=MAIN/SNOMEDCT-SE/2025-05-31&release=&languages=sv,en

- **PLAX**  
  Parasternal long axis, a view that shows the heart from the left side and visualizes the left atrium, mitral valve, left ventricle, aortic valve, and ascending aorta.

- **PSAX**  
  [text]

- **2 chamber**  
  Apical 2-chamber view (A2C) visualizes the left atrium (LA) and left ventricle (LV) in a longitudinal section, specifically the anterior and inferior walls of the left ventricle.

- **3 chamber**  
  Apical long axis view. It visualizes the left ventricle, left atrium, and aortic root (including the aortic valve).

- **4 chamber**  
  Visualizes the left atrium, right atrium, left ventricle, and right ventricle.

- **5 chamber**  
  Shows the four chambers plus the aorta.

  - **Subcostal**  
  [text]

## Cardiac Cycle Phase
The measurement is taken during or in a specific part of the heart's cycle.

**openEHR**: Because the cardiac cycle phase very rarely varies for the same parameter, we have chosen not to represent it as a separate attribute under State. Instead, it is specified directly within the attribute for the measurement value under Items.

- **End systole**  
  The phase in the heart cycle when the ventricles have contracted maximally and emptied of blood, just before they begin to relax.

- **End diastole**  
  The end of the heart cycle's relaxation and filling phase, just before the heart muscle begins to contract (systole).

- **Systole**  
  The phase in the heart cycle when the heart contracts to pump out the blood.

- **Diastole**  
  The phase in the heart cycle when the heart muscle relaxes and the heart chambers fill with blood.

## Physical Quantity
Quantity measured on a certain body structure. The measurement can be "indexed," meaning the value is divided by body surface area.

**openEHR**: Quantity + structure will become attributes under `Items` in the cluster archetype.

- **Volume**  
  Volume in a cavity in the heart, e.g., ventricle or atrium.  
  **How it's measured**: Calculated for the left ventricle either with Simpson's method/biplane method of discs or measured in 3D-mode for both left and right ventricles. Also from 2D single plane — how?

- **Ejection fraction**  
  The heart's pumping ability, i.e., how much of the heart's diastolic volume is pumped out with each heartbeat.  
  **How it's measured**: Calculated and based on volume either from biplane-mode or measured in 3D-mode (also M-mode [Wikipedia link]).

- **Diameter**  
  Thickness of a structure.  
  **How it's measured**: Measured in M-mode or 2D. Can be indexed.

- **Thickness**  
  Thickness of a structure.  
  **How it's measured**: Measured in M-mode or 2D.

- **Mass**  
  Weight of a structure in the heart.  
  **How it's measured**: Calculation (Devereux method) based on a measurement in 2D-mode of the structure's diameter.

- **Area**  
  Area of a structure in a certain view.  
  **How it's measured**: Measured by tracing the surface.

- **Velocity**  
  Speed at which blood flows or a muscle moves.  
  **How it's measured**: Blood is measured with spectral Doppler and muscle with tissue Doppler.

- **Pressure**  
  [Text]

## Exertion
Degree of exertion. There is a cycle machine that the patient can lie in during the examination.

**openEHR**: Since this describes a condition of the patient, it should be expressed under `State` in the observation archetype. There is an archetype, `CLUSTER.level_of_exertion.v0`, that could be used but there is no slot for it at the moment.

## Calculation
There are different ways of calculating values, including:

- **Indexed values**  
A measurement may be indexed, meaning that the value has been divided by the patient's body surface area (BSA).

  We have chosen not to perform this calculation at the time of data retrieval but instead to include the indexed value directly in the archetype. This is to avoid the risk of errors arising from any subsequent recalculation.

- **Values calculated during a measurement**  
Simpson's method (biplane method of discs) (volume)  
This method is used to calculate left ventricular volume and is also subsequently used in the calculation of the ejection fraction.

- **Values calculated from previously performed measurements**  
Devereux method (mass)  
This method is used to calculate left ventricular mass based on measurements that have already been obtained.

**openEHR:** This is currently represented through specific elements in CLUSTER.imaging_exam_us_technique.v0.

## Estimation
An estimated value of a quantity derived from the measurement of another quantity. The result is based on broad categorizations as well as the clinician’s expert knowledge and experience.

## Draft openEHR

<img width="1480" height="1142" alt="image" src="https://github.com/user-attachments/assets/03a58dbb-1536-4dc7-b95c-f17d79864763" />


**OBSERVATION.imaging_exam_result.v1**

State

The State section in the observation archetype consists of three attributes: Confounding factors, Position, and Stabilising appliance. We need to be able to specify the level of exertion. This could be recorded using Confounding factors, but since there is already a cluster archetype, `CLUSTER.level_of_exertion.v0`, we would like to see a dedicated slot for Exertion.

The patient's position is not something that the Department of Clinical Physiology documents during an echocardiographic examination.

**CLUSTER.imaging_exam_heart.v0**

This archetype is a specialization of the CLUSTER archetype `openEHR-EHR-CLUSTER.imaging_exam.v1`. In addition to the attributes inherited from the parent archetype, it contains attributes for measurement values that includes the part of the heart on which the measurement was performed, the measured quantity (volume, area, pressure, etc.), and the phase of the cardiac cycle.

In the current draft of the archetype, there are 38 measurement values from an echocardiographic examination, which are being used in a Proof of Concept  in Region Östergötland. This selection is intended to reflect the measurements typically performed during a standard examination. The plan is to expand this to approximately 100 measurements in order to better capture all measurement values that may be obtained during an echocardiographic examination.

A decision was made not to divide the archetype into multiple specializations for different parts of the heart. This eliminates the problem of having parameters that do not belong to a single structure, or cases where only a single measurement value exists for a particular cardiac structure and would therefore require its own archetype specialization.

**CLUSTER.imaging_exam_us_technique.v0**

This archetype is intended to hold information about the technical conditions of an ultrasound measurement and is intended to be placed in the Structured technique/procedure slot of the archetype `openEHR-EHR-OBSERVATION.imaging_exam_result.v1`.

It will contain attributes for View, Mode, 2D Method, Doppler Method, and Algorithm. All attributes have internally coded value sets with options specifically tailored for echocardiographic examinations. These value sets can be overridden when the archetype is used within a template.


