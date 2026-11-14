# Ghost Hunter Pro — Product Requirements (Draft 0.1)

## Product stance

A professional Android field-investigation instrument and evidence-management app. It uses a phone's available sensors to measure, record, correlate, and review environmental signals that investigators may find relevant. It must **not** claim that a phone can scientifically detect, identify, or communicate with paranormal entities: no validated method establishes that. The app can support an investigator's exploration and documentation, while clearly distinguishing measured data from interpretation. It must never fabricate readings, label noise as a spirit, or imply that an anomalous reading proves a haunting.

**Product promise:** “A rigorous field kit for capturing what happened, where, and under what conditions—so investigators can review evidence rather than rely on memory.”

**Primary users:** experienced paranormal investigators; investigation teams; researchers and skeptical reviewers. Secondary: hobby investigators seeking a responsible, transparent tool.

**Platforms:** native Android; Kotlin; Android sensor APIs; phones and tablets. Android version range and minimum hardware to be decided after device/API survey.

## Goals and non-goals

### Goals
- Capture synchronized, time-stamped environmental sensor data with provenance and understandable limitations.
- Make field sessions usable in darkness, with gloves, and without network access.
- Record audio, video, notes, locations, and investigator actions alongside sensor timelines.
- Support repeatable investigation protocols, team collaboration, and exportable evidence packages.
- Be transparent about missing sensors, device variability, permissions, calibration, and uncertainty.
- Protect sensitive location and recording data by default.

### Non-goals / prohibited claims
- No assertion of verified paranormal detection, spirit identification, or two-way communication.
- No “spirit box” audio manipulation marketed as entity speech; no randomized words, synthetic voices, or algorithmic speech attribution.
- No false precision, hidden smoothing, fabricated sensor readings, or unexplained “entity score.”
- No medical, safety, or emergency guidance based on sensor readings. The app is not a substitute for gas, fire, structural, or other certified safety equipment.

## Core user journeys
1. **Prepare:** create a case, choose a protocol, verify permissions and sensor availability, inspect battery/storage, and run a sensor self-check.
2. **Investigate:** start a session, see live sensor status and elapsed time, make timestamped notes/bookmarks, capture media, and mark investigator actions or environmental changes.
3. **Review:** replay recordings and sensor traces on a common timeline, inspect provenance and data gaps, compare observations, and annotate possible mundane explanations.
4. **Share:** export a portable, privacy-reviewed case bundle with original files, metadata, and an integrity manifest; optionally share with team members.

## Functional requirements

### 1. Case and session management
- Cases contain title, site description, optional address/coordinates, consent/access notes, team, equipment, and investigation protocol.
- Sessions contain start/end times, device model/OS/app version, sensor inventory, permission state, location mode, and investigator roster.
- Support offline creation and capture; queue optional sync until the user chooses to connect.
- Session states: setup, recording, paused, completed, interrupted/recovered. Explain interruptions and never silently imply continuous capture.
- Autosave notes and session state; recover safely after process death, reboot, or storage pressure where Android permits.

### 2. Hardware inventory and sensing
Discover sensors at runtime; never assume every Android device has every sensor. Show availability, vendor/name, reported range/resolution, sampling rate, and limitations. Use public Android APIs and respect background-execution restrictions.

Candidate inputs:
- **Magnetic field sensor (magnetometer):** three-axis field readings in microtesla where supported; show axes, magnitude, range/clipping, and sensor accuracy status. Clearly identify nearby electronics, steel, cases, and charging as likely confounders.
- **Accelerometer and gyroscope:** motion/orientation context, useful for detecting device handling and stabilizing interpretation—not paranormal indicators.
- **Ambient light sensor:** lux if present; distinguish missing sensor from dark conditions.
- **Proximity sensor:** raw/near-far status when available; note that many are short-range and binary.
- **Barometer:** pressure in hPa when present; distinguish local pressure changes from altitude/weather effects.
- **Temperature/humidity:** usually unavailable as true ambient measurements on phones; do not misrepresent battery or internal temperature as room temperature. Support optional external Bluetooth instruments later with device/source labels.
- **Microphone:** user-controlled audio capture; preserve original audio. Optional waveform/spectrum and event markers can assist review, but no speech/EVP claim without transparent, independently testable processing.
- **Camera:** user-controlled photo/video; preserve capture metadata where permitted; no automatic “apparition” labeling.
- **GNSS/location:** optional coarse or precise location, explicit consent, privacy warning, and geotag controls.
- **Wi-Fi/Bluetooth/cellular:** do not imply radio strength or network scans detect entities. Any future use must be opt-in, legal, clearly described as RF/environmental context, and subject to OS access restrictions.
- **Flashlight, screen, vibration, speaker, compass:** utility/navigation only. Never represent generated tones or vibration as entity communication.

Sensor capture requirements:
- Record monotonic elapsed timestamps and wall-clock mapping; retain original samples and sampling metadata.
- Show actual sampling rate, gaps, dropped samples, accuracy/uncalibrated state, clipping, and permission/background limitations.
- Allow per-sensor start/stop, sample-rate presets within OS/device capability, and visible battery/storage cost estimates.
- Avoid continuous sensor use when not actively recording. Explain foreground-service notifications and OS restrictions where applicable.
- No automatic “normal/abnormal” verdict. If highlighting unusual changes, use configurable, documented statistical descriptions (e.g. deviation from that session's baseline), not paranormal classification.

### 3. Recording and evidence timeline
- Separate controls for audio, video, photos, and sensor streams; visible active-recording indicator and persistent notification when required.
- Timeline combines sensor readings, media start/stop, notes, bookmarks, location fixes, and manually logged events, all with source and timestamp.
- Add a one-tap marker with optional label, voice note, or text note. Provide a quiet/haptic confirmation option.
- Preserve source media unchanged. Any derived waveform, spectrogram, filtered view, or enhancement is a separate derivative with processing settings and link to original.
- Support media playback with synchronized timeline cursor and adjustable playback speed.

### 4. Field UX and tools
- Dark, high-contrast interface with large touch targets and configurable red/low-light display mode; no flashing effects.
- Readable live dashboard, compact mode, sensor cards, and customizable layout. Include accessibility support and screen-reader labels.
- Compass/orientation view must disclose calibration status and interference; no decorative “entity radar.”
- Audio playback and analysis are review tools only. No randomized frequency sweeps, spirit-word dictionaries, or generated responses.
- Optional checklist templates (baseline sweep, room-by-room, environmental log) and investigator-defined prompts that do not suggest leading questions.

### 5. Review, analysis, and reporting
- Graph raw sensor data with units, axis controls, time range, gaps, and event overlays. Display provenance and sensor limits on demand.
- Provide descriptive analysis only: min/max/mean, distribution, rate of change, clipping/gap counts, and comparison to a user-selected baseline. Explain algorithms and never label results paranormal.
- Allow annotations for competing explanations (device handling, HVAC, vehicles, nearby electrical equipment, weather, investigator movement, recording artifacts).
- Case report includes methods, device/sensor inventory, calibration/self-check results, session conditions, permissions, known data gaps, original/derived media index, annotations, and user conclusions explicitly marked as interpretation.
- Export machine-readable CSV/JSON for sensor data plus human-readable PDF/HTML report and a portable archive. Include a manifest with hashes for integrity verification; hashes establish file integrity, not truth/authenticity of an event.

### 6. Calibration and quality
- Provide guided sensor checks and orientation/zero-baseline procedures only where meaningful. Do not describe software self-checks as certified calibration.
- Record calibration/accuracy status, method, timestamp, and known limitations. Support external calibrated instruments as future integrations.
- Include a pre-session checklist: permissions, storage, battery, sensor inventory, clock, device placement, nearby sources, and consent.
- Provide a protocol for repeat measurements and controlled baselines; preserve raw data even if a user changes visualization settings.

### 7. Privacy, security, and consent
- Local-first storage; no account required for basic use. Encryption at rest for sensitive app data where practical, Android backup behavior disclosed, and secure deletion limitations explained.
- Explicit runtime permission prompts with just-in-time rationale. No recording or location access without user action and permission.
- Recording consent checklist and jurisdiction reminder; avoid legal guarantees.
- Exports default to excluding precise coordinates, personal names, and device identifiers unless selected. Preview the export contents before sharing.
- No ads or third-party analytics SDKs that receive case content/location. Crash reporting, if any, must be opt-in or privacy-preserving and never include recordings or case details.
- Clear data retention, backup, deletion, and optional sync policy. Team sharing uses explicit invitations/access controls and revocation.

## Non-functional requirements
- Reliable operation offline and graceful recovery from interruptions.
- Sensor and media timestamps aligned as closely as Android APIs permit; document clock and synchronization error rather than promise impossible precision.
- Minimize battery, thermal load, and storage; warn before long sessions, low storage, and thermal throttling.
- No network requirement for capture, playback, or export.
- Localization-ready units, dates, and text; SI units by default with optional alternatives.
- Accessibility: TalkBack, scalable text, high contrast, color-independent status indicators, reduced motion.
- Test on a representative device matrix, including devices with missing sensors, varying Android versions, and restrictive background behavior.

## Proposed release scope

### Release 1 — dependable field recorder
- Case/session setup, runtime sensor inventory, magnetometer/accelerometer/gyroscope/light/barometer when available, audio recording, photos, timestamped notes/markers, offline use, live status, raw-data timeline, basic graphs, CSV/JSON + report export, permission/privacy controls, recovery and data-gap reporting.
- No paranormal classifications, communications, cloud sync, or automated speech interpretation.

### Release 2 — team and review workflow
- Video capture, synchronized playback, richer annotations, protocol templates, team sharing, report customization, archive integrity manifests, external sensor integrations, and expanded device QA.

### Later, evidence-led options
- Optional transparent audio analysis and external instrument integrations only after requirements are validated with investigators and researchers. Each algorithm needs reproducible documentation, test data, limitations, and a clear distinction between measured signal and interpretation.

## Acceptance criteria for Release 1
- On unsupported hardware, missing sensors are clearly shown as unavailable; no fabricated or substituted values appear.
- Every recorded sample/event is traceable to a source, timestamp, unit, and session; gaps and interruptions are visible in both UI and export.
- Recording indicators and permission states are unambiguous; stopping the app or denying a permission does not create misleading “complete” data.
- Original audio/photo files remain unmodified; derived views are labeled and reproducible.
- Offline session capture, review, and export work without network access.
- Export preview makes sensitive fields visible and lets the user omit them.
- All app copy avoids asserting paranormal proof or communication; sensor descriptions include common confounders and limitations.
- Automated and manual tests cover sensor absence, permission denial/revocation, storage exhaustion, process death, timestamp gaps, and low battery.

## Product decisions to validate with users
1. Is the primary buyer an individual investigator, a team, or an investigation organization?
2. Is fully local storage the default even if that limits cross-device collaboration? (Recommended: yes.)
3. Should Release 1 record audio continuously for long sessions, or prioritize sensor logs plus investigator-triggered clips?
4. Which external instruments are most commonly used and have documented APIs (EMF meters, environmental meters, recorders)?
5. Which Android minimum version and supported device classes are commercially important?
6. Is a subscription acceptable for team sync/reporting, or should the product be a one-time purchase?

## Risks and mitigations
- **Scientific credibility risk:** users may interpret correlation as proof. Mitigate with neutral labels, raw data, transparent methods, confounder guidance, and no paranormal score.
- **Hardware variability:** sensors differ or may be absent/un calibrated. Detect at runtime, report metadata, and test broadly.
- **Battery/privacy risk:** long recordings consume resources and capture sensitive information. Explicit controls, persistent indicators, local-first design, estimates, and export review.
- **Expectation mismatch:** “communicate with entities” is not a validated capability of smartphone hardware. State this plainly in onboarding and marketing; offer timestamped observation prompts and playback rather than simulated communication.
- **Safety risk:** investigators may use the phone instead of safety equipment. Repeatedly clarify that it is not a gas, fire, electrical, or structural safety detector.

## Open question for the product owner
Should the app's positioning explicitly be “evidence-first paranormal investigation” (recommended), or should it remain a neutral environmental recording toolkit marketed to paranormal investigators? Either way, the product must not claim validated entity detection or communication.
