# Phase 1️⃣ — Final Report

## Demonstration Description

### Introduction

!!! question "What is the demonstration about? Describe it in a few sentences as if explaining to a non-specialist."

As a new demonstration for the [Mobile Photonics Bike](https://www.thorlabs.com/mobile-photonics-lab---europe), we propose **two setups** based on the [Light Commands study](https://lightcommands.com/) in which the injection of voice commands into smart appliances using a light source modulated with an audio signal.

The **first setup** would utilise a collimated LED as its light source, and target a microphone connected to an amplifier and oscilloscope. This demonstration is focused on the first principles of modulating a signal from one medium to another, and illustrating the notion of signal quality.

The **second setup** would utilise a laser source to activate a smart target (home assistant, smartphone...), reproducing the results of the [original study](https://arxiv.org/pdf/2006.11946). The choice of a laser source is justified by the variance in the reported minimum power required for voice command injection at 30cm distance for different devices, ranging from 0.5mW for a Google Home to 60mW for a Samsung Galaxy S9. Thus, this demo is initially designed for a worst case scenario of 60mW activation power, and is designed to be fully enclosed to maximise safety.  

---

### Pedagogical Goals

!!! question "What concepts in optics and photonics does this demonstration illustrate? What should a member of the public take away from it?"

- **Showcase** how a signal carrying information (in our case a voice command) can be carried over different media (acoustic, electronic, optical), and what mechanisms are used to convert from one medium to another (microphone, optical modulation).
- **Introduce** the notion of *signal to noise ratio*, **explain** how the power per surface area at the target impacts this metric, and **demonstrate** what influences this metric (input power, beam focus, distance to target). 

**Recommanded pedagogical material**

We recommand creating laminated cards explaining the operating principle of various components used in the demo. This includes:

- MEMS Microphones.
- LED and Laser diodes.
- Collimation.
- Signal to noise ratio.

---

### Session Description

!!! question "Describe what a typical session looks like: how is the equipment set up, what does the demonstrator do, what does the audience see and interact with?"

**Setup**

- The team sets up the two demos on opposite ends of the Mobile Photonics Lab, and performs the necessary alignment using personal protective equipment (PPE).
- Before the sessions starts, all the features of the demos are tested as a final rehearsal, with particular emphasis on testing laser safety features.

**Demo 1 - LED light source to Microphone**

1. A signal (coming from a microphone, a recorded audio, or a signal generator) is modulated onto the light of a collimated LED and directed onto a microphone connected to an amplifier and an oscilloscope, which is used to visualise the received signal.
2. By changing the input power of the LED and/or the beam width, the impact of these parameters on the signal quality is illustrated.

**Demo 2 - Laser light source to Smart Target**

1. With the enclosure opened, the different components of the demonstration are explained to the attendees.
2. After closing the enclosure, the laser source is turned on, and a voice command signal (coming from a microphone or a recorded audio file) is modulated onto the amplitude of the continuous wave, hitting the microphone of a smart target (Smartphone or home assistant). We envision this smart target to be connected to a peripheral (such as a smart lamp) to make the demonstration more interactive.
3. By changing the input power of the laser, the notion of the minimum activation power is demonstrated.

---

## Parts List

### System Description

!!! question "Provide a high-level description of the full system architecture: how do the transmitter, receiver, and surrounding hardware work together?"

Both demos share the same underlying signal chain: an electrical audio signal is used to drive the optical output power of a light source (LED or laser), which is shaped and aimed by free-space optics, then converted back into an electrical/acoustic signal by a MEMS microphone diaphragm at the receiver.

**Demo 1 - LED light source to Microphone**

The **transmitter (Tx)** takes an audio signal from one of three interchangeable sources — a live microphone, a pre-recorded voice command, or a signal generator (used to inject test tones for the SNR demonstration) — and feeds it to an **LED driver**, which converts the electrical waveform into a proportional drive current. This modulates the optical output power of the **LED** in amplitude, encoding the audio signal onto the light itself. A **diaphragm** placed after the LED acts as an adjustable aperture, giving a second, independent control over the optical power reaching the target (in addition to the LED driver's electrical gain). A **collimator** then narrows the diverging LED output into a roughly parallel beam so that optical power stays concentrated over the free-space path to the receiver.

The **receiver (Rx)** is simply a **microphone and amplifier**: the modulated light strikes the microphone's diaphragm directly, which responds to the intensity fluctuations of the light in the same way it would to an acoustic pressure wave (the same photoacoustic/photothermal coupling exploited in the original LightCommands attack). The amplifier boosts this recovered signal and feeds it to an **oscilloscope**, so the audience can directly see the transmitted waveform being reconstructed. Because every stage (source, LED driver, diaphragm aperture, collimation, distance) is exposed and independently adjustable, this setup is used to illustrate how each parameter affects **signal-to-noise ratio** at the receiver.

```mermaid
flowchart LR
    Source --> LDR[LED driver]
    LDR --> LED
    subgraph Tx
        direction LR
        LED[LED] -.-> DPG[Diaphragm]
        DPG -.-> COL[Collimator]
    end
    subgraph Rx
        direction LR
        MIC[Microphone and amplifier]
    end
    COL -.-> MIC
    MIC--> Oscilloscope
```

**Demo 2 - Laser light source to Smart Target**

Demo 2 follows the same source → driver → emitter → collimator → receiver logic as Demo 1, but replaces the LED with a **laser** to reach the higher optical power which might be needed to activate a real device, and replaces the exposed microphone with a **smart target** (smartphone or home assistant). The laser driver, laser, and collimator direct a modulated beam across a short free-space path onto the smart target's built-in MEMS microphone, which decodes the light modulation as if it were a spoken voice command. Once the target's voice assistant recognises the injected command, it drives a connected **peripheral** (e.g. a smart plug, light, or the device's own speaker/screen) to visibly confirm activation to the audience.

Because the laser is driven at powers up to the worst-case 60 mW design point, the entire **Tx** and **Rx** are housed inside a shared **enclosure**, integrating a **laser safety panel** (rated to the source's wavelength) and an **interlock switch**  wired into the laser driver's interlock input.  This lets the demonstrator open the enclosure to explain the components to the audience, then close it before energising the laser, keeping the beam fully contained during operation. 

```mermaid
flowchart LR
    Source --> LDR[Laser Driver]
    LDR --> INT{Interlock closed?}
    subgraph Enclosure
        direction LR
        INT -- yes --> LAS[Laser]
        subgraph Tx
            direction LR
            LAS -.-> COL[Collimator]
        end
        subgraph Rx
            direction LR
            SMT[Smart target]
        end
        COL -.-> SMT
    end
    SMT --> Peripheral
    
```

---

### Transmitter Parts

!!! question "List all parts used in the transmitter (Tx), including model numbers where known."

**Audio source**

| Demo | Part | Model / Reference | Notes |
|------|------|-------------------|-------|
| **1** | Signal generator | Can borrow equipment at UCL, but **TBD** for other locations. There are very cheap [DIY kits](https://www.amazon.co.uk/DollaTek-Precision-Generator-5Hz-400kHz-Adjustable/dp/B09CG1CXYH/ref=sr_1_5?crid=HSIXNLDP1BDF&dib=eyJ2IjoiMSJ9.0wtKxKN72szg-TBBLvVFWWx8Ml_8r-wb9LO1yBC1cuip71xQr3pBLIT9DBrAD68a7a1hGDjS_MEHpctRzXuT7UKpF-mYZbaLrkUK7FRqh9GTpfncs6D_03Xw402tjHWLsns367T0KSDMoXU4E1ZIJbKt6MVlol_Mqe2QkL5qGeT39d-LZg0fzldsoSWiewwvCK2kSRwvietpAE6CoIlNjFxqr01DYd9-GJBLQ0SMoOEEbVac18v3hFsLOvXeZtcWHqPVhS2nXo1Oi86-X8F4nv3bRlFoA07hgyVQwPYnOes.Ud-Y-VMjtMCEFLxm8dl2aUI4EacsEs0R6zN4r9GaGOw&dib_tag=se&keywords=diy+signal+generator&qid=1786961400&sprefix=diy+signal+generator%2Caps%2C124&sr=8-5) on Amazon. | Used to modulate pure tones to illustrate signal to noise ratio considerations.  |
| **1&2** | Computer with audio file | | Connected to an amplifier through a jack cable. |
| **1&2** | Microphone | [MEMS microphone](https://www.sparkfun.com/sparkfun-analog-mems-microphone-breakout-sph8878lr5h-1.html?srsltid=AfmBOorJR_O9TRLpsM3VKT8S3gT8oLNcQGy8QEvru-dUsHdxy7WYczSl) | Used in the Lightcommands study. |
| **1&2** | Jack to breadboard connector | | Connects the MEMS microphone to the audio amplifier. |
| **1&2** | Microphone amplifier | [With speaker](https://www.aliexpress.com/item/1005008978691693.html?src=google&src=google&albch=shopping&acnt=603-455-9033&isdl=y&slnk=&plac=&mtctp=&albbt=Google_7_shopping&aff_platform=google&aff_short_key=_oFgTQeV&gclsrc=aw.ds&albagn=888888&ds_e_adid=&ds_e_matchtype=&ds_e_device=c&ds_e_network=x&ds_e_product_group_id=&ds_e_product_id=en1005008978691693&ds_e_product_merchant_id=5558341424&ds_e_product_country=GB&ds_e_product_language=en&ds_e_product_channel=online&ds_e_product_store_id=&ds_url_v=2&albcp=23634837834&albag=&isSmbAutoCall=false&needSmbHouyi=false&gad_source=1&gad_campaignid=23634872088&gbraid=0AAAABCRFad-11uVnMhmVAd1T4jeV-ae9r&gclid=Cj0KCQjw4orUBhCjARIsAIbF3qxqYTl5ywh0K1r1bAmPTsok-qVuDO4BY-u9vgjxIne6pBxGSMCLEW0aAqI9EALw_wcB), [Commercial amplifier](https://www.amazon.com/gp/product/B01MS22YWV?th=1) | The Commercial amplifier is the one used in the Lightcommands study, and can be connected to either the microphone or a computer playing an audio file. |

!!! note "Prototyping before Phase 2"
    The custom interface stage that converts the audio source (microphone, audio file, or signal generator) into the 0-5V analogue signal fed to the LED/laser driver's modulation input is not an off-the-shelf part, and will be prototyped and tested at UCL ahead of Phase 2.

**Optical modulation**

| Demo | Part | Model / Reference | Notes |
|------|------|-------------------|-------|
| **1** | LED Driver | [CD40](https://www.thorlabs.com/4.0-a-led-driver) or [T-Cube™ LED Driver](https://www.thorlabs.com/t-cube-tm-led-driver) | Modulation input connected to analogue source delivering a 0-5V signal. |
| **1** | LED | [M450LP2](https://www.thorlabs.com/item/M450LP2) | Need a visible light LED which can achieve reasonably high power in order to achieve reasonable SNR|
| **1** | LED Cage Plate mount with SM1 thread | [CP33/M](https://www.thorlabs.com/item/CP33_M) | |
| **1** | Diaphragm with SM1 threads | [SM1D12](https://www.thorlabs.com/item/SM1D12)| Used as an additional control for LED Power|
| **1** | Collimation adaptor with SM1 thread| [SM1U25-A](https://www.thorlabs.com/item/SM1U25-A) | Preferably a zoom housing in order to demonstrate the impact of beam focus on received signal.|
| **2** | Laser Driver | [LDC205C](https://www.thorlabs.com/item/LDC205C) | Modulation input connected to analogue source delivering a 0-5V signal, and interlock pin connected to interlock lever switch.|
| **2** | Laser diode | **TBD** | Must reach 60mW of power. However not sure which to choose. Visible light would be easier to align at low power, but far IR would be more safe. |
| **2** | Strain relief cable to DB8| [SR9A-DB9](https://www.thorlabs.com/item/SR9A-DB9) | Need the correct pin code to interface with diode|
| **2** | Cage Plate Collimation Mount | [LDH56-P2/M](https://www.thorlabs.com/item/LDH56-P2_M) | |


---

### Receiver Parts

!!! question "List all parts used in the receiver (Rx), including the target voice-activated device and any supporting hardware."

**Demo 1 — Microphone & mounting**

| Demo | Part | Model / Reference | Notes |
|------|------|-------------------|-------|
| **1** | Microphone | [ADMP401](https://www.amazon.com/SparkFun-MEMS-Microphone-Breakout-INMP401/dp/B004TGZJ1G) | Same part as used in the original LightCommands study. The receiver team has some alternative MEMS mic candidates in mind in case this one is hard to source. |
| **1** | Dovetail optical rail | [RLA600/M](https://www.thorlabs.com/item/RLA600_M) (600 mm) or [RLA900/M](https://www.thorlabs.com/item/RLA900_M) (900 mm) | Length depends on how much room is available on the bike. The mic slides along this rail towards/away from the beam to show, live, that SNR and the waveform on the scope visibly degrade with distance — the main teaching moment of this station, so the mount is designed around it. |
| **1** | Rail carrier | [RC2/M](https://www.thorlabs.com/item/RC2_M) | Sliding element on the dovetail rail that carries the microphone back and forth along the beam axis. |
| **1** | Transverse rail carrier | [RC3](https://www.thorlabs.com/item/RC3) | Clamps onto the main rail and provides a dovetail perpendicular to it, for coarse lateral adjustment to centre the mic in the beam. |
| **1** | Custom 3D-printed mic adapter | Custom (team-built) | Adapts the ADMP401 breakout board onto the rail carrier or an optical post; not a Thorlabs part. |
| **1** | Amplifier table clamp | [CL5A](https://www.thorlabs.com/item/CL5A) | L-shaped table clamp used to fix the audio amplifier to the breadboard. |
| **1** | Audio amplifier | [With speaker](https://www.aliexpress.com/item/1005008978691693.html?src=google&src=google&albch=shopping&acnt=603-455-9033&isdl=y&slnk=&plac=&mtctp=&albbt=Google_7_shopping&aff_platform=google&aff_short_key=_oFgTQeV&gclsrc=aw.ds&albagn=888888&ds_e_adid=&ds_e_matchtype=&ds_e_device=c&ds_e_network=x&ds_e_product_group_id=&ds_e_product_id=en1005008978691693&ds_e_product_merchant_id=5558341424&ds_e_product_country=GB&ds_e_product_language=en&ds_e_product_channel=online&ds_e_product_store_id=&ds_url_v=2&albcp=23634837834&albag=&isSmbAutoCall=false&needSmbHouyi=false&gad_source=1&gad_campaignid=23634872088&gbraid=0AAAABCRFad-11uVnMhmVAd1T4jeV-ae9r&gclid=Cj0KCQjw4orUBhCjARIsAIbF3qxqYTl5ywh0K1r1bAmPTsok-qVuDO4BY-u9vgjxIne6pBxGSMCLEW0aAqI9EALw_wcB), [Commercial amplifier](https://www.amazon.com/gp/product/B01MS22YWV?th=1) | Used to amplify the audio signal, to be connected to a speaker and/or an oscilloscope|
| **1** | Oscilloscope | Can borrow equipment at UCL, but **TBD** for other locations. There are very cheap [DIY kits](https://www.amazon.co.uk/Treedix-Oscilloscope-Handheld-Real-Time-Sampling/dp/B0C85S78GY/ref=sr_1_5?crid=1NEUBW09IQYA7&dib=eyJ2IjoiMSJ9.H9DIHbhw4FeyXoXASVAe4XSv9G3WjfCGlMXlogTJOvTjj2r_osEPlKB1wgHY-HqAUgDXL7--KPd6ddFmYNmDUVJ-7fGv_BmLUz4qOMc1RdyiwGN74Dpc4GWP0fFS2dIqSEiIGYlAt7v_RS30HoF_w_UFoBepo_54g9E-iIGFS5LVrzqLsxREZH7YBAMFdxq-E9gdWAcnTZymJI6oLLPAWBmKr6D4aoV49dw4T5M79KVEVjdCzAbUgmk8sPp0WVrIGkuBickgcMx1jzMBKlUjQcZ6sg4qLJ3cxi9CSohFX0M.tTTN_dSwMImGVhltdT_G6N1H4WQZsTWXdkQuAeXl0vk&dib_tag=se&keywords=diy+oscilloscope&qid=1786961372&sprefix=DIY+osc%2Caps%2C125&sr=8-5) on Amazon. | Used to visualise the received signal, and perform spectral analysis to illustrate signal to noise ratio considerations. |

**Demo 2 — Target & peripheral**

| Demo | Part | Model / Reference | Notes |
|------|------|-------------------|-------|
| **2** | Smart target — Plan 1 | **TBD**: Google Home | The most sensitive device reported in the original study (0.5 mW at 30 cm, vs. 60 mW for a Samsung Galaxy S9), which keeps our required laser power lowest. Worth adding to the ask list for Thorlabs, to see if they'd be willing to provide one. Also needs a 3D-printed holder for the device. |
| **2** | Smart target — Plan 2 | Volunteer's phone | Fallback if a Google Home isn't available. Doable, but needs significantly more power to activate. |
| **2** | Stage for the target | **TBD** | 3D-printed holder needed to safely align the target's microphone with the laser beam. |
| **2** | Peripheral (visible confirmation) | e.g. TP-Link Kasa/Tapo smart plug or bulb | Voice command (e.g. "turn on the lamp") drives this so the audience gets a clear, visible confirmation the target was activated. Relies on Wi-Fi, since the assistant sends the audio to the cloud for recognition — plan is to bring our own hotspot. |
| **2** | Local voice-assistant fallback (no internet) | Raspberry Pi running Home Assistant + local wake word engine + Zigbee bulb | Bypasses the Google/Alexa cloud entirely so the whole recognition-to-peripheral chain stays on LAN. More setup work than the hotspot plan, kept on the table as a fallback for venues with no internet access at all. |

!!! note "Prototyping before Phase 2"
    The custom receive chain from the microphone through to the oscilloscope, the 3D-printed mic adapter and target stage, and the local voice-assistant fallback, are not off-the-shelf parts, and will be prototyped and tested at UCL ahead of Phase 2.

---

### Other Parts (Mounts, Enclosure, etc.)

!!! question "List all remaining parts: optical mounts, breadboard, enclosure, cables, and anything else required to assemble the full system."

| Demo | Part | Model / Reference | Notes |
|------|------|-------------------|-------|
| **2** | NIR Detector Card | [VRC7](https://www.thorlabs.com/item/VRC7) | Used at low power to align the laser with the target and demonstrate the presence of IR light (if we use a NIR diode). |
| **2** | Enclosure | [XE25C11T/M](https://www.thorlabs.com/item/XE25C11T_M) | Top open, with laser safety panel facing the public.|
| **2** | Laser Safety Panel | [LWxP2/M](https://www.thorlabs.com/item/LW1P2_M)| Exact panel will depend of wavelength of laser |
| **2** | Interlock system | [Lever switch](https://www.amazon.co.uk/Gebildet-pieces-Miniature-Switch-Momentary/dp/B07T9DWMMG/ref=asc_df_B07T9DWMMG?mcid=f01cee05a660392c83d310c43db39473&tag=googshopuk-21&linkCode=df0&hvadid=697363582268&hvpos=&hvnetw=g&hvrand=12826283976019115331&hvpone=&hvptwo=&hvqmt=&hvdev=c&hvdvcmdl=&hvlocint=&hvlocphy=9045885&hvtargid=pla-783906794563&hvocijid=12826283976019115331-B07T9DWMMG-&hvexpln=0&gad_source=1&th=1) + [2.5mm jack connector](https://www.digikey.co.uk/en/products/detail/tensility-international-corp/053-0280R/701163?gclsrc=aw.ds&gad_source=1&gad_campaignid=23249465655&gbraid=0AAAAADrbLlgrKaT7nPn8TNfSxlsX8dlEd&gclid=Cj0KCQjwv4XUBhDBARIsAE6bQUSy7EdxlOymtTAqSwjYG2OdEJeFpZBuJbX0XvQ_-qaeP-_sBIK-icoaAg55EALw_wcB) | Thorlabs laser drivers seem to all use 2.5mm jack interlock inputs |
| **1&2** | Optical breadboards (x2) | [MB4560/M](https://www.thorlabs.com/item/MB4560_M) | The enclosure for demo 2 is 525mmx375mm, but demo 1 could use a smaller breadboard |
| **1&2** | Optical posts, post holders & bases | [TR75/M](https://www.thorlabs.com/item/TR75_M) post + [PH75/M](https://www.thorlabs.com/item/PH75_M) post holder + [BA2/M](https://www.thorlabs.com/item/BA2_M) base | Used both on the dovetail rail and directly on the breadboard. UCL's 6th floor lab may already have some of these — worth checking before ordering. |

---

## UCL Risk Assessment

!!! question "Complete the UCL risk assessment for the demonstration. Identify each hazard, its likelihood and severity, and the mitigations in place."


**Laser classification (Setup 2)**

Per [BS EN 60825-1](https://www.gov.uk/government/publications/laser-radiation-safety-advice/laser-radiation-safety-advice#fn:2), a bare/embedded emitter at 60mW is a **Class 3B laser**: it is well above the Class 1/1M/2/2M/3R accessible emission limits for the near-infrared, but stays below the 500 mW CW threshold separating Class 3B from Class 4. Class 3B means direct intrabeam viewing and specular reflections are hazardous to the eye (and, to a lesser extent, the skin), while diffuse reflections are normally safe.

Because the laser diode, and beam path are fully housed inside the interlocked [enclosure](#other-parts-mounts-enclosure-etc), the demonstration as a whole is designed and operated as a **Class 1 laser product**: under normal operating conditions (enclosure closed, interlock made), there is no accessible emission above Class 1 limits anywhere the audience or demonstrators can be. The embedded Class 3B engine is only ever accessible with the enclosure open, during which the laser is de-energised or run at minimum power for alignment, as described in the [Session Description](#session-description).

**Safety measures in place for Setup 2**

- **Full enclosure** ([XE25C11T/M](https://www.thorlabs.com/item/XE25C11T_M)) housing the entire beam path from laser to target, so the 980 nm beam is never accessible during normal operation.
- **Hardware interlock** (switch + 2.5 mm jack wired into the [LDC205C](https://www.thorlabs.com/item/LDC205C) driver's interlock input) that disables laser emission the instant the enclosure is opened — enforced by the driver itself, not by software or operator discipline.
- **Laser safety panel** ([LW2P2/M](https://www.thorlabs.com/item/LW1P2_M), OD 6 at 980 nm, i.e. transmission ≈ 10⁻⁴ %) facing the public, attenuating any residual/scattered light to well below Class 1 exposure limits even if viewed directly.
- **Low-power alignment procedure**: the beam is invisible (980 nm), so alignment and re-alignment are always performed at minimum drive current using the [VRC7](https://www.thorlabs.com/item/VRC7) NIR detector card to visualise the beam, never by eye.
- **Trained operators only**: the laser is powered up and adjusted only by briefed demonstrators; the public only ever interacts with the smart target and its peripheral, never with the beam path itself.
- **Pre-session checks**: interlock function and enclosure integrity are tested as part of the final rehearsal before every session (see [Session Description](#session-description)).

| Hazard | Likelihood | Severity | Mitigation |
|--------|-----------|---------|------------|
| Direct or specularly-reflected exposure to the Class 3B, 980 nm laser beam (eye/skin injury) | Low | High | Beam fully enclosed during operation; hardware interlock cuts laser power the instant the enclosure is opened; alignment done at minimum power with an IR detector card, never by eye. |
| Interlock failure or bypass, allowing the enclosure to be opened while the laser is energised | Low | High | Interlock wired directly into the driver's hardware interlock input (fails safe, not software-controlled); function-tested before every session as part of the final rehearsal. |
| Residual beam or reflection escaping via the enclosure's open top | Low | Medium | Beam path kept low within the enclosure, well below the top rim; laser safety panel attenuates the forward-facing side; demonstrators do not reach over the open top while the laser is energised; warning signage on the enclosure. |
| Invisible beam causing unaware exposure during setup/alignment if IR laser diode is used | Low | Medium | NIR detector card ([VRC7](https://www.thorlabs.com/item/VRC7)) used to visualise and align the beam at minimum power before any full-power operation; PPE (IR-rated laser safety eyewear) worn during alignment. |
| Electric shock or fire from mains-powered laser/LED drivers, amplifier, and oscilloscope | Low | Medium | Only PAT-tested Thorlabs/lab bench equipment used; cables routed and strain-relieved away from foot traffic; all equipment powered down between sessions; no modification of mains wiring. |
| Manual handling injury while lifting/mounting the optical breadboards and enclosure onto the Mobile Photonics Bike | Medium | Medium | Two-person lift for breadboards and enclosure; equipment secured to the bike's designed mounting points before travel; team briefed on manual handling technique beforehand. |
| Trip or entanglement hazard from cabling and equipment in a public walkway | Medium | Low | Cables routed behind the breadboards and taped down; demonstration area kept clear of the public path; demonstrators stationed at each setup throughout the session. |
| Unsupervised public contact with laser hardware or its enclosure | Low | Medium | Enclosure keeps all laser hardware inaccessible to the public; a demonstrator is present at Setup 2 at all times; public interaction limited to the peripherals outside the enclosure. |
| Eye exposure to the visible LED beam in Setup 1 | Low | Low | LED (Class 1/2 equivalent, well below laser AELs); beam intentionally aimed away from the public; brief, supervised exposure only. |

!!! warning "This section must be approved by UCL before the demonstration can take place."
