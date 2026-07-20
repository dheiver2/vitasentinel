# 🛡️ VitaSentinel

**Patient Fall & Posture Monitoring** — pose-estimation model watches patient position around the clock and flags falls or unsafe movement instantly.

VitaSentinel augments human pose estimation (via the [OpenPifPaf](https://github.com/openpifpaf/openpifpaf) library) with multi-camera, multi-person tracking and a long short-term memory (LSTM) neural network that classifies each tracked person as **Fall** or **No Fall** in real time. Five temporal and spatial features are extracted from the estimated body keypoints on every frame and fed into the LSTM classifier — no wearables, no extra hardware, just a camera feed.

<p align="center">
<img src="examples/fall.gif" width="420" />
</p>

## Why VitaSentinel

- **24/7 unattended monitoring** — a fixed or PTZ camera watches the room continuously; no staff member needs to be present.
- **Instant alerting** — a fall is flagged the moment it's detected, not after the fact.
- **Multi-patient, multi-camera** — tracks several people across several video sources at once.
- **Runs on CPU** — no GPU required for a pilot deployment (`--disable_cuda`).

## Setup

```shell script
python3 -m venv venv && source venv/bin/activate
pip install -r requirements.txt
```

## Usage

```shell script
python3 fall_detector.py --video path/to/video.mp4 --save_output --disable_cuda
```

<TABLE>
<TR><TH style="width:120px">Argument</TH><TH style="width:300px">Description</TH><TH>Default</TH></TR>
<TR><TD>num_cams</TD> <TD>Number of Cameras/Videos to process</TD><TD>1</TD></TR>
<TR><TD>video</TD><TD>Path to the video file (None to capture live video from camera(s)) <br>For single video fall
                        detection(--num_cams=1), save your videos as abc.xyz
                        and set --video=abc.xyz<br> For 2 video fall
                        detection(--num_cams=2), save your videos as abc1.xyz
                        & abc2.xyz & set --video=abc.xyz</TD><TD>None</TD></TR>
<TR><TD>save_output</TD> <TD>Save the result in a video file. Output videos are
                        saved in the same directory as input videos with "out"
                        appended at the start of the title</TD><TD>False</TD></TR>
<TR><TD>disable_cuda</TD> <TD>To process frames on CPU by disabling CUDA support on GPU</TD><TD>False</TD></TR>
</TABLE>

## Dataset

The LSTM classifier was trained on the [UP-Fall Detection](https://sites.google.com/up.edu.mx/har-up/) dataset. See [this Colab notebook](https://colab.research.google.com/drive/1PbzVZnwBzFK_CcMf5G3dFrjwKZgfK3Vy?usp=sharing) to download the dataset and compile the files into videos.

## Credits & Attribution

VitaSentinel is a rebranded fork of [**HumanFallDetection**](https://github.com/taufeeque9/HumanFallDetection) by **Mohammad Taufeeque and Samad Koita**, distributed under the MIT License (see [LICENSE](LICENSE)). All core pose-estimation, tracking and LSTM classification logic is theirs — this fork only changes branding, packaging and adds a demo landing page. Please cite their paper if this work helps your research:

> Mohammad Taufeeque, Samad Koita, Nicolai Spicher, Thomas M. Deserno. *"Multi-camera, multi-person, and real-time fall detection using long short term memory."* Medical Imaging 2021: Imaging Informatics for Healthcare, Research, and Applications, SPIE, 2021. [doi:10.1117/12.2580700](https://doi.org/10.1117/12.2580700)

```bibtex
@inproceedings{Taufeeque2021MulticameraMA,
                author = {Mohammad Taufeeque and Samad Koita and Nicolai Spicher and Thomas M. Deserno},
                title = {{Multi-camera, multi-person, and real-time fall detection using long short term memory}},
                volume = {11601},
                booktitle = {Medical Imaging 2021: Imaging Informatics for Healthcare, Research, and Applications},
                organization = {International Society for Optics and Photonics},
                publisher = {SPIE},
                pages = {35 -- 42},
                year = {2021},
                doi = {10.1117/12.2580700},
                URL = {https://doi.org/10.1117/12.2580700}
              }
```

## License

MIT — see [LICENSE](LICENSE). Copyright retained by the original authors; VitaSentinel branding and landing page © 2026.
