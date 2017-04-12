Swift project containing the work of Steven Sawtelle's Fulton Undergraduate Research Intiative project for the Spring of 2017. The aim of this project is to create a Swift wrapper of the National Instruments Virtual Instrument Software Architecture (VISA) standard. Funded by Arizona State University and mentored by Dr. Owen Hildreth

How to install:

- Download the three visa header files: visa.h, visatype.h, and vpptype.h

- Create new XCode project

- Choose macOS, and then Command Line Tool as the template of your project

- Name it whatever, for the purposes of this sample tutorial we will call it SwiftVISA

- Name and bundle are unimportant, fill in as necessary for your project

- Make sure the language is Swift

- Save it where you prefer, and create Git repo if you'd like(generally recommended)

- Drag in the 3 files from before (visa.h, visatype.h, vpptype.h) into the same folder as contains the auto-generated main.swift file

- Ensure Copy items if needed is checked, Create folder references is marked, and the name of your project is checked as a target in Add to targets

- Select the folder containing these (should now be 4) files, and go to File->New->...

- Under macOS, select "Header File" as the template, and click Next

- Save as you'd like (for this example, we will say SV-Bridging-Header.h). This file will serve as the bridging header between your C headers and Swift files. 

- Make sure the name of your project is selected as a target, and press Create

- After the line of #define YOUR-BRIDGING-HEADER and above #endif, insert the following 3 lines:

#import "visa.h"
#import "visatype.h"
#import "vpptype.h"

- Save the file

- Select your main project in the project explorer, and create a new group named visa (this should be on the same level as the folder containing the header files and main.swift)

- Create a new file inside this group, and under macOS select Empty as the template. Save it as module.map, and again make sure it is applied to your project name as a target

- Paste the following into your new module.map file, with PATH_TO_REPOSITORY replaced as apropriate(mine is "/Users/stevensawtelle/Developer"):

module visa [system] {
    header "PATH_TO_REPOSITORY/SwiftVISA/visa.h"
    header "PATH_TO_REPOSITORY/SwiftVISA/visatype.h"
    header "PATH_TO_REPOSITORY/SwiftVISA/vpptype.h"
    export *
}

- Select your main project in the project explorer again, then in the main window select Build Settings

- Under Swift Compiler - Search Paths, create a new Import Paths entry that looks like this, where PATH_TO_REPOSITORY is the same as before:

PATH_TO_REPOSITORY/SwiftVISA

- Under Swift Compiler - General, create a new entry for Objective-C Bridging Header named
