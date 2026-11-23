# 7. Data Ethics and Confidentiality

Lab projects use public data, licensed commercial data, and administrative data about people. Each kind carries different rules. Breaking them can end a project, cost the lab its access to data, and harm the people the data describe. Read this document before you receive any project data.

## Kinds of data and their rules

| Kind of data | Examples | Main rules |
|---|---|---|
| Public | Census tables, Statistics Canada releases, open city data | Cite the source. Follow the terms of use. |
| Licensed | Retail scanner data, commercial property data | Only people named in the licence may see the data. Some licences limit access to graduate researchers. Do not copy the data to personal devices, cloud tools, or AI tools. The provider may need to review results before release. |
| Administrative or confidential | Shelter records, student records, health records | Ethics approval may be required. Store only on approved systems. Report results only at a level that cannot identify a person. |

Ask your supervisor which category your project's data falls into. If you are not sure, treat the data as confidential.

## Research involving people

The University of Toronto requires that all research involving human participants be reviewed and approved by the relevant Research Ethics Board (REB) before work begins. This applies to student research whether or not it is funded. The requirement comes from the Tri-Council Policy Statement (TCPS 2), which covers research with human participants and their data at institutions eligible for federal research funding.

Every lab member who handles data about people completes the TCPS 2: CORE-2022 tutorial (<https://tcps2core.ca/>), which is free and online. The supervisor keeps the certificates on file. Some secondary data, such as anonymized public-use files, may be exempt from REB review. The supervisor decides, with the REB where needed, whether approval is required.

## Identifiers

Personal information can identify someone directly or indirectly. Direct identifiers include a name, a phone number, or a government ID number. Indirect identifiers, such as month and year of birth, nationality, or gender, can identify a person when combined. J-PAL's guide to de-identification gives a full list and recommends encrypting identifying data as early as possible in the project (Kopper, Sautmann, and Turitto, 2020).

- Remove or encrypt direct identifiers before analysis, following the supervisor's instructions.
- Never try to identify a person from the data, even out of curiosity.

## Storage and sharing

- Store project data only in the location your supervisor names. Do not keep copies on USB drives, personal cloud accounts, or shared computers.
- Never upload licensed or confidential data to an AI tool, a website, or a public repository ([Document 8](08-ai-use-policy.md)).
- Do not email data files. Share a link to the approved folder.
- When your appointment ends, delete any local copies and confirm this in your exit checklist ([Document 13](13-closing-packet.md)).

## Reporting results

- Do not report cells with very small counts that could identify a person or a small group. Follow the threshold set by the data provider. If there is none, the lab's default is a minimum of 10 observations per cell.
- Do not describe individual cases in a way that someone could recognize, even without a name.
- Some licences require the provider to review results before publication. Check before you present any result outside the lab, including at the lab seminar.

## If something goes wrong

If data is lost, shared by mistake, or seen by someone who should not see it, tell your supervisor the same day. Early reporting lets the lab limit the damage and meet any reporting duties to the data provider or the University. You will not be penalized for reporting an honest mistake.

## Sources

- University of Toronto, School of Graduate Studies. "Research Involving Human Participants: Overview." <https://www.sgs.utoronto.ca/policies-guidelines/research-involving-human-participants/>
- Panel on Research Ethics. TCPS 2: CORE-2022 (Course on Research Ethics). <https://tcps2core.ca/>
- Kopper, S., Sautmann, A., and Turitto, J. (2020). *J-PAL Guide to De-Identifying Data*. J-PAL Global. <https://www.povertyactionlab.org/media/file-research-resource/guide-de-identifying-data>
- Shen, J., and Vilhuber, L. "Physically Protecting Sensitive Data." In *Handbook on Using Administrative Data for Research and Evidence-based Policy*. <https://admindatahandbook.mit.edu/>
