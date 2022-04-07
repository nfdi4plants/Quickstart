<img src="media/image1.png" alt="drawing" width="200"/>

# DataPLANT’s QuickStart on ARCs

> V1.1, 2022

We are very happy that you chose our tools and infrastructure to create
and share your own ARCs. In this QuickStart we focus on how to use the
ARC Commander and SWATE to store your data and enrich it with metadata.

This document is work in progress: If you experience any
inconsistencies, have questions or would like to suggest additions to
it, please feel free to send a message to: info@nfdi4plants.org.

- [Setup and environment](#setup-and-environment)
  - [Required softwares](#required-softwares)
  - [The command line](#the-command-line)
- [ARC initialization](#arc-initialization)
- [Adding metadata](#adding-metadata)
  - [ISA investigation](#isa-investigation)
  - [ISA studies and assays](#isa-studies-and-assays)
- [Sharing your ARC](#sharing-your-arc)
  - [DataPLANT registration and access](#dataplant-registration-and-access)
  - [ARC synchronization](#arc-synchronization)
  - [Invite collaborators](#invite-collaborators)
- [Data annotation](#data-annotation)
  - [SWATE](#swate)

## Setup and environment

### Required softwares

- [ ] Please download the latest version of the [ARC Commander](https://github.com/nfdi4plants/arcCommander/releases) for your operating system and install it according to [these instructions](https://github.com/nfdi4plants/arcCommander#install-and-start).
- [ ] Prerequisites for using the ARC Commander are [git](https://git-scm.com/downloads) and [git LFS](https://git-lfs.github.com/)

### The command line

- Most of this quickstart (especially the section [ARC initialization](#arc-initialization)) is based on the command line (Windows: cmd, powershell; Linux and Mac: terminal). The following picture shows exemplarily how to open a powershell on windows by entering *powershell* into the explorer path:  

  <img src="media/image2.png" alt="drawing" width="400"/>

- Text formatted as code blocks represents commands to copy/paste into the command line:

```bash
echo "hello - I am a code block"
```

<div style="page-break-after: always;"></div>

## ARC initialization

1. Create and navigate to a local folder, which you want to initialize as an ARC.

```bash
mkdir ~/QuickStartARC; 
cd ~/QuickStartARC
```

1. Test if the ARC Commander is functional by displaying the ARC commander version and help menu:

  ```bash
  arc --version
  arc --help
  ```
  
  <img src="media/image3.png" alt="drawing" width="400"/>

1. Initialize your ARC by executing
  
  ```bash
  arc init
  ```

1. This will create the general ARC folder structure:

    <img src="media/image4.png" alt="drawing" width="400"/>
    <img src="media/image5.png" alt="drawing" width="400"/>

<div style="page-break-after: always;"></div>

## Adding metadata

### ISA investigation

The ISA investigation workbook allows you to record administrative metadata of your project. Add the isa.investigation.xlsx workbook including an identifier to your ARC with

  ```bash
  arc i create -i “QuickStartInvestigation”
  ```

### ISA studies and assays

The ISA study and ISA assay workbooks allow you to annotate your experimental data.

1. Add an isa.study.xlsx workbook including an identifier to your ARC with

  ```bash
  arc s create -s “QuickStartStudy”
  ```
  
2. Add an isa.assay.xlsx workbook including an identifier to your ARC with

  ```bash
  arc a create -s “QuickStartStudy” -a “QuickStartAssay”
  ```

> Note: An assay must be linked to a study. If a study does not exist, it will be created automatically in this step.

- The ARC Commander will add a subdirectories to the *studies* and *assays* folder. Your ARC should
    look similar to this now:  

    <img src="media/image6.png" alt="drawing" width="400"/>

- These steps can be repeated to add as many studies and assays as needed.
    Accordingly, more subdirectories will be added. Multiple assays can be grouped in a study when the
    same StudyIdentifier in the text editor window is used.

Place the data for each assay in the respective dataset folder.

<div style="page-break-after: always;"></div>

## Sharing your ARC

### DataPLANT registration and access

In case you are not a member of DataPLANT yet, please visit <https://register.nfdi4plants.org> to register. Afterwards, you will be granted access to DataPLANT’s DataHUB, available under <https://git.nfdi4plants.org>.
The DataHUB allows you to share your ARCs with registered lab or project partners.

<img src="media/image7.png" alt="drawing" width="400"/>

After successful registration, please visit the [DataHUB](https://git.nfdi4plants.org) to set an access token for
ARC Commander synchronization:

1. Sign-in in the top right corner. Click on your profile picture in the top right corner and go to *Preferences -\> Access Tokens.*

2. Create an api access token with a name of your choice. These tokens grant read and write access to all of your groups and projects. Make sure you save your access token upon successful creation, as this is the only time you will have access to the token (in case you lose the token, you can simply create a new one).

<img src="media/image8.png" alt="drawing" width="400"/>
<img src="media/image9.png" alt="drawing" width="400"/>

### ARC synchronization

1. Open the ARC Commander within your ARC as described above.
    Synchronize your ARC with the DataHUB using the command `arc
    sync`. The ARC Commander will ask for your credentials, where you
    need to enter your DataHUB handle (displayed on the DataHUB when
    clicking on your profile picture) and the newly generated access
    token.

    1. If you did not connect your local ARC with a remote so far,
        you can specify the remote address with the flag -r in
        combination with a URL, e.g.,  
        `arc sync -r git@git.nfdi4plants.org:brilator/quickstart.git`  

       <img src="media/image10.png" alt="drawing" width="400"/>

    2. In case you want to create a new remote repository at this
        URL, it needs to be assembled like the following example:  
        <https://git.nfdi4plants.org/>*YourUserName*/*NameOfLocalFolder*

        If no repository exists under the given URL, the ARC Commander
        will produce an error ensuring that you spelled the URL
        correctly**.** Use `arc sync -f` to force synchronization to
        the specified URL.

        <img src="media/image11.png" alt="drawing" width="400"/>

> Note: In case you did not set your git user name and email
    address you might get a warning to do so. These are needed for
    displaying them on the git commits. You can update the settings with
    the following commands:
    `git config --global user.name <your_name>`  
    `git config --global user.email <your_email>`

1. Check if the upload was successful by visiting the respective URL.

   <img src="media/image12.png" alt="drawing" width="400"/>

### Invite collaborators

1. You can invite lab-colleagues or project partners to join your ARC
    for collaborative work. While inside your ARC on the DataHUB, click
    on *Project information -\> Members* in the left navigation panel.
    Search for registered researchers and select a role for each
    individually. These roles come along with different rights. In
    short:  
    *Guest:* Have the least rights. Advised to use this for people you
    are asking for consultancy. *Developer:* The choice for most people
    you want to invite to your ARC. Developers have read and write
    access, but cannot maintain the project on the DataHUB, e.g.
    inviting others.  
    *Maintainer:* Gives the person the same rights as you have (except
    of removing you from your own project). This is recommended for
    inviting PIs or group leaders allowing them to add their group
    members for data upload or analysis to the project as well.  
    <img src="media/image13.png" alt="drawing" width="400"/>

> Note: A detailed usage instruction for the ARC Commander can be found
> [here](https://github.com/nfdi4plants/arcCommander/wiki/Detailed-usage-instruction).

<div style="page-break-after: always;"></div>

## Data annotation

Your ARC should now contain one isa.investigation.xlsx and one or
    more isa.study.xlsx and isa.assay.xlsx file(s), respectively. Use
    the isa.study.xlsx to describe the characteristics of your samples,
    e.g. how you grew your plant, and isa.assay.xlsx to annotate
    experimental analyses.

### SWATE

DataPLANT provides the Excel Add-In SWATE to support you in data annotation.

- [ ] Download and install the newest SWATE version according to [these instructions](https://github.com/nfdi4plants/Swate/wiki/docs01-installing-Swate#desktop-installation).
- [ ] In case you use an Excel version older than Excel 2019, please install [SWATE for Excel online](https://github.com/nfdi4plants/Swate/wiki/docs01-installing-Swate#quickstart).

- Use the *create annotation table* button in the yellow pop-up box
    (this only appears if you start SWATE on an Excel worksheet without
    an existing annotation table). An annotation table with the building
    blocks *Source Name* and *Sample Name* will be generated.  

   <img src="media/image14.png" alt="drawing" width="400"/>
   <img src="media/image15.png" alt="drawing" width="400"/>

- Annotate your table with help of the [annotation principles](https://nfdi4plants.github.io/AnnotationPrinciples/). In short, *Characteristics* are used for study descriptions and describe inherent properties of the source material (e.g. a certain strain). *Parameters* describe steps in your experimental workflow (e.g. an instrument model or a growth chamber), and *Factors* describe independent variables that result in a specific output
    (e.g. the light intensity).

- The combination of ISA (Characteristics, Parameter, Factor) and
        a biological or technological ontology (e.g. temperature,
        strain, instrument model) gives the flexibility to display an
        ontology term, e.g. temperature, as a regular process parameter
        or as the factor your study is based on (Parameter
        \[temperature\] or Factor \[temperature\]).

- Customize your table by adding building blocks:

    1. Choose the type of building block you want to add (A).

    2. If you chose a descriptive building block type (building blocks
        besides Sample Name, Source Name, and Data File Name), use
        search field (B) to search for an Ontology Term. SWATE accesses
        the SwateDB with a list of established external ontologies
        designated suitable for use in plant science. In addition, we
        feature our own ontology NFDI4PSO to extend the DB with missing,
        but necessary terms.

    3. If you want to add a building block with a unit, check box (C)
        and use search field (D) to look for a fitting unit term, e.g.
        degree Celsius as unit for Parameter \[temperature\].

    4. If you could not find a fitting term, you can use the Advanced
        Term Search with the blue links above the *Add building block*
        button. If you still could not find a fitting term, use free
        text input.  

        <img src="media/image16.png" alt="drawing" width="400"/>

    5. For more information on customizing your annotation table click
        [here](https://github.com/nfdi4plants/Swate/wiki/Docs03-Building-Blocks).

1. Alternatively, you can also use one of DataPLANT’s [SWATE
    templates](https://github.com/nfdi4plants/Swate/wiki/Docs05-Templates).
    You can find them under the *Protocol Insert* tab in SWATE.  

    <img src="media/image17.png" alt="drawing" width="400"/>

2. Fill the cells beneath each building block with ontology terms to
    note the respective *Characteristics, Parameter,* and *Factor*
    values of your experiment. Using the ontology term search function,
    you can fill multiple cells at once.

    1. When *Use related term directed search* (A) is enabled, SWATE
        will suggest a selection of suitable terms within the ontology
        for the column header, e.g. *TripleTOF* *5600* for *instrument
        model.*

    2. When term directed search (A) is disabled, SWATE will still
        suggest ontology terms, but without relation to the column
        header.

    3. If you could not find a fitting term, use free text input.

    <img src="media/image18.png" alt="drawing" width="400"/>
    <img src="media/image19.png" alt="drawing" width="400"/>

*More information on how to use SWATE can be found
[here](https://github.com/nfdi4plants/Swate/wiki/Docs05-Templates).*

**In case you need further assistance also visit our
[Helpdesk](https://support.nfdi4plants.org).**
