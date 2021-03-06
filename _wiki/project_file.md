---
title: 'Project File'
redirect_from: '/wiki/Project_File'
---
The project file is used to provide the information about your project
to mothur needed to build your submission data. Columns should be tab
delimited. You can download this file [
here](https://mothur.s3.us-east-2.amazonaws.com/wiki/test.project.zip).

## Submission Name

The submission name is your NCBI login username. This field is required.

    Username yourNCBIUserName

## Last Name

The last name of the submission owner. This field is required.

    Last yourLastName

## First Name

The first name of the submission owner. This field is required.

    First yourFirstName

## Email

The email address to inform about updates related to the submission.
This field is required.

    Email youremail@email.com

## Center Name

The name of center or University used when you registered at the SRA.
This field is required.

    Center University of Michigan

## Type

The type of Institute the center is. This field is required. Options
are: consortium, center, institute and lab. This is a controlled
vocabulary section in the XML file that will be generated.

    Type Institute

## Ownership

Valid ownership options are owner or participant. This is a controlled
vocabulary section in the XML file that will be generated. This field is
not required, owner is the default.

    Ownership owner

## website

The website of the project or your lab. This field is optional.

    website www.yourWebsite.org

## Project Name

This is the name of your project. This field is required.

    ProjectName development of murine micro biome

## Project Title

This is the title of your project. This field is required.

ProjectTitle Stabilization of the murine gut microbiome following
weaning

## Description

The description of your project. This field is required.

    Description Here we describe the dynamics of a self-contained community, the murine gut microbiome. Using 16S rRNA gene sequencing of fecal samples collected daily from individual mice, we characterized the community membership and structure to determine whether there were significant changes in the gut community during the first year of life. Based on analysis of molecular variance, we observed two community states.

## Grant

This is used to provide information about grants associated with the
project. You may enter multiple grants, one per line. The id and agency
fields are required if you provide a grant. The title field is optional.

    Grant id=R01HG005975, agency=National Institutes of Health, title=Identifying Population-level Variation in Cross-sectional and Longitudinal HMP St
