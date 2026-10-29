# When to Eat

**Know What's in Your Fridge — a food storage tracking prototype with reusable RFID tokens**

2024 KAIST Makerathon **Grand Prize · KRW 2,500,000** | Team **The Old Man and Go**

[![Prototype with a refrigerator mockup, RFID token storage box, and food tracking GUI](media/previews/prototype-overview.jpg)](media/photos/prototype/prototype-system-overview-01.jpeg)

[Demo](#demo) · [Final Presentation](DesignAndPresentation/when-to-eat-final-presentation.pptx) · [Photo and Video Catalog](media/README.md)

## Overview

When to Eat helps older adults keep track of the food in their refrigerator and how long it has been stored. Reusable RFID tokens with food illustrations attach to containers. A reader in the token storage box works with a desktop interface to show which containers are in use and how many storage days remain.

We built and demonstrated a refrigerator mockup, illustrated tokens and attachments, an RFID reader setup, and a Windows food tracking GUI at the makerathon.

## How It Works

1. **Choose a token.** Take a token matching the food category out of the RFID storage box.
2. **Attach it to a container.** Once the token is no longer detected in the box, the container appears in the active list and its storage timer starts.
3. **Check and return.** Check the remaining days on the screen. After using the food, return the token to the box to remove it from the active list and prepare it for reuse.

### Token Attachments

| Lid attachment | Container-side attachment |
| :---: | :---: |
| [<img src="media/previews/token-lid-attachment.jpg" alt="Vegetable token attached to a food container lid" width="300">](media/photos/attachments/vegetable-token-on-container-lid-01.jpeg) | [<img src="media/previews/token-side-attachment.jpg" alt="Meat token attached to the side of an acrylic container" width="300">](media/photos/attachments/meat-token-on-container-side-01.jpeg) |

The presentation proposes a silicone cover attachment for different container shapes and a magnetic attachment for containers. Food illustrations identify the category, while border colors help distinguish tokens.

## Demo

### RFID Reader and Food Tracking Interface

The GIF below previews the approximately 12-second portrait demo. Click it to open the original MOV with audio.

[<img src="media/previews/rfid-reader-and-gui-demo.gif" alt="Demo panning from the RFID token storage box to the food list on a laptop" width="300">](media/videos/demo/rfid-reader-and-gui-demo.mov)

[Original demo](media/videos/demo/rfid-reader-and-gui-demo.mov) · [Early food list update test](media/videos/demo/food-list-update-test.mov) · [Event videos](media/README.md#videos)

### Food Tracking GUI

![GUI showing food categories, token colors, purchase dates, discard dates, and remaining days](media/previews/food-tracking-dashboard.png)

*Demo screenshot from the final presentation. Food icon rendering is commented out in the source currently included in this repository.*

- Displays the active container count and food list, sorted by remaining days.
- Shows the food category, token color, start date, scheduled discard date, and remaining days.
- Uses **red for overdue items, yellow for 0–2 days remaining, and green for 3 or more days remaining**. These status colors are separate from the token border colors.
- Displays the reader connection, operation, and battery status.

## Team and Award

[![Four team members with the completed prototype and Grand Prize board](media/previews/team-grand-prize.jpg)](media/photos/awards/team-with-prototype-landscape.jpeg)

| Team member | Role |
| --- | --- |
| Sangeon Jeon | Team leader |
| Sehyeon Kim | Team member |
| Byeongyoung Jeong | Team member |
| Yujin Park | Team member |

We won the Grand Prize at the 2024 KAIST Makerathon. The [original award board photo](media/photos/awards/grand-prize-board.jpeg) shows the prize amount of **KRW 2,500,000**.

## Repository Structure

```text
.
├── Code/                         # Windows UWP C# / XAML source
├── DesignAndPresentation/        # Final presentation and fabrication drawings
│   ├── when-to-eat-final-presentation.pptx
│   ├── TokenDesign.pdf
│   └── Model Refrigerator Lasar Cutting View.pdf
├── media/
│   ├── README.md                 # Source names, current paths, and descriptions
│   ├── photos/                   # 26 original photos
│   │   ├── development/
│   │   ├── tokens/
│   │   ├── attachments/
│   │   ├── prototype/
│   │   ├── awards/
│   │   └── event/
│   ├── videos/                   # 4 original videos
│   │   ├── demo/
│   │   └── event/
│   └── previews/                 # README photos, GIF, and GUI image
├── KAIST Makerathon.pptx          # Early concept presentation
├── KAIST Makerathon (2).pptx      # Additional planning presentation
└── KAIST Makerathon.pdf           # Planning document
```

| Resource | Contents |
| --- | --- |
| [Final presentation](DesignAndPresentation/when-to-eat-final-presentation.pptx) | Problem, user workflow, implementation, and future plans |
| [Token design](DesignAndPresentation/TokenDesign.pdf) | Token fabrication design |
| [Refrigerator mockup drawing](DesignAndPresentation/Model%20Refrigerator%20Lasar%20Cutting%20View.pdf) | Laser cutting drawing for the mockup |
| [Photo and video catalog](media/README.md) | Media grouped by scene, with source names and descriptions |

## Software and Setup

The GUI uses **Windows UWP, C#, and XAML**, communicating with an **ATID ATD100 UHF RFID reader** through a virtual COM port. The interface is defined in [MainPage.xaml](Code/MainPage.xaml), and token state and food list management are implemented in [ReaderViewModel.cs](Code/ReaderViewModel.cs).

This repository does not include the `.sln`, `.csproj`, app manifest, or ATID SDK, so it cannot be built on its own. The previous setup instructions point to a base project in this [Google Drive folder](https://drive.google.com/drive/folders/18IRY2AfHl9cmScwam55FEvZh57e8WAxe).

1. Prepare a Windows environment with Visual Studio support for UWP development, the original UWP project, and a compatible ATID SDK.
2. Replace the corresponding files in the base project with the files in `Code/`.
3. Connect the reader and identify its COM port. The default in the source is `COM6`; update the configuration and sample RFID identifiers to match your hardware and tokens.
4. Launch the app, select the reader, and use **Connect → Inventory6c** to connect and start scanning.

### Current Implementation Scope

The source uses 12 sample tokens and fixed storage durations for demonstration. The list is managed in memory; database persistence is not included. The barcode decoding callback is unimplemented.

**Refrigerator alerts, a mobile app or widget, and additional token types** are future plans described in the presentation.
