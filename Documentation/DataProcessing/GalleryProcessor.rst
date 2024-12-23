:navigation-title: gallery
..  include:: /Includes.rst.txt
..  _GalleryProcessor:

========================
`gallery` data processor
========================

The :php:`\TYPO3\CMS\Frontend\DataProcessing\GalleryProcessor`,
alias `gallery`, provides the logic for working with galleries and
calculates the maximum asset size. It uses the files already present in
the `processedData` array for its calculations. The :ref:`FilesProcessor` can
be used to fetch the files.

..  contents:: Table of contents

..  _GalleryProcessor-options:

Options:
========

..  confval-menu::
    :display: table
    :type:
    :Default:

    ..  _GalleryProcessor-if:

    ..  confval:: if
        :name: GalleryProcessor-if
        :Required: false
        :type: :ref:`if` condition
        :Default: ''

        Only if the condition is met the data processor is executed.


    ..  _GalleryProcessor-filesProcessedDataKey:

    ..  confval:: filesProcessedDataKey
        :name: GalleryProcessor-filesProcessedDataKey
        :Required: true
        :type: :ref:`data-type-string` / :ref:`stdWrap`
        :Default: 'files'
        :Example: 'myImages'

        Key of the array previously processed by the :php:`FilesProcessor`.


    ..  _GalleryProcessor-numberOfColumns:

    ..  confval:: numberOfColumns
        :name: GalleryProcessor-numberOfColumns
        :Required: false
        :type: :ref:`data-type-integer` / :ref:`stdWrap`
        :Default: field:imagecols
        :Example: 4

        Expects the desired number of columns. Defaults to the value of the field
        `imagecols` (:guilabel:`Number of Columns`) if used with content elements.

    ..  _GalleryProcessor-mediaOrientation:

    ..  confval:: mediaOrientation
        :name: GalleryProcessor-mediaOrientation
        :Required: false
        :type: :ref:`data-type-integer` / :ref:`stdWrap`
        :Default: field:imageorient
        :Example: 2

        Expects the image orientation as used in the field `imageorient` in content
        elements such as text with images. Defaults to the value of the field
        `imageorient` (:guilabel:`Position and Alignment`) if used with content
        elements.

        ..  include:: /Images/AutomaticScreenshots/Fluidtemplate/ImageOrientation.rst.txt

    ..  _GalleryProcessor-maxGalleryWidth:

    ..  confval:: maxGalleryWidth
        :name: GalleryProcessor-maxGalleryWidth
        :Required: false
        :type: :ref:`data-type-integer` / :ref:`stdWrap`
        :Default: 600

        Maximal gallery width in pixels.

    ..  _GalleryProcessor-maxGalleryWidthInText:

    ..  confval:: maxGalleryWidthInText
        :name: GalleryProcessor-maxGalleryWidthInText
        :Required: false
        :type: :ref:`data-type-integer` / :ref:`stdWrap`
        :Default: 300

        Maximal gallery width in pixels if displayed in a text.

    ..  _GalleryProcessor-equalMediaHeight:
    ..  _GalleryProcessor-equalMediaWidth:

    ..  confval:: equalMediaHeight, equalMediaWidth
        :name: GalleryProcessor-equalMediaHeight
        :Required: false
        :type: :ref:`data-type-integer` / :ref:`stdWrap`
        :Default: field:imageheight, field:imagewidth
        :Example: 300

        If set all images get scaled to a uniform height / width. Defaults
        to the value of the fields `imageheight` (:guilabel:`Height of each element
        (px)`), `imagewidth` (:guilabel:`Width of each element (px)`) if used with
        content elements.

        ..  include:: /Images/AutomaticScreenshots/Fluidtemplate/MediaHeight.rst.txt

    ..  _GalleryProcessor-columnSpacing:

    ..  confval:: columnSpacing
        :name: GalleryProcessor-columnSpacing
        :Required: false
        :type: :ref:`data-type-integer` / :ref:`stdWrap`
        :Default: 0
        :Example: 4

        Space between columns in pixels

    ..  _GalleryProcessor-borderEnabled:

    ..  confval:: borderEnabled
        :name: GalleryProcessor-borderEnabled
        :Required: false
        :type: :ref:`data-type-integer` / :ref:`stdWrap`
        :Default: field:imageborder
        :Example: 1

        Should there be a border around the images? Defaults to the value of the
        fields `imageborder` (:guilabel:`Number of Columns`) if used with content
        elements.

    ..  _GalleryProcessor-borderWidth:

    ..  confval:: borderWidth
        :name: GalleryProcessor-borderWidth
        :Required: false
        :type: :ref:`data-type-integer` / :ref:`stdWrap`
        :Default: 0
        :Example: 2

        Width of the border in pixels.

    ..  _GalleryProcessor-borderPadding:

    ..  confval:: borderPadding
        :name: GalleryProcessor-borderPadding
        :Required: false
        :type: :ref:`data-type-integer` / :ref:`stdWrap`
        :Default: 0
        :Example: 20

        Padding around the border in pixels.


    ..  _GalleryProcessor-cropVariant:

    ..  confval:: cropVariant
        :name: GalleryProcessor-cropVariant
        :Required: false
        :type: :ref:`data-type-string` / :ref:`stdWrap`
        :Default: "default"
        :Example: "mobile"

        See :ref:`crop variants in the TCA reference <t3tca:columns-imageManipulation-properties-cropVariants>`

    ..  _GalleryProcessor-as:

    ..  confval:: as
        :name: GalleryProcessor-as
        :Required: false
        :type: :ref:`data-type-string` / :ref:`stdWrap`
        :Default: "files"

        The variable name to be used in the Fluid template.

    ..  _GalleryProcessor-dataProcessing:

    ..  confval:: dataProcessing
        :name: GalleryProcessor-dataProcessing
        :Required: false
        :type: array of :ref:`dataProcessing`
        :Default: []

        Array of data processors to be applied to all fetched records.

..  _GalleryProcessor-example-rows-columns:

Example: display images in rows and columns
===========================================

Please see also :ref:`dataProcessing-about-examples`.

..  rubric:: TypoScript

As the :php:`GalleryProcessor` expects the data of the files to be
present in the the `processedData` array, the :php:`FilesProcessor`
always has to be called first. Execution depends on the key in the
:ref:`dataProcessing <GalleryProcessor-dataProcessing>` array, not the order in
which they are put there.

The content of :ref:`filesProcessedDataKey <GalleryProcessor-filesProcessedDataKey>`
in the :php:`GalleryProcessor` has to be equal to the content of
:ref:`as <FilesProcessor-as>` in the :ref:`FilesProcessor <FilesProcessor>`:

..  include:: /CodeSnippets/DataProcessing/TypoScript/GalleryProcessor.rst.txt

..  rubric:: The Fluid template

..  include:: /CodeSnippets/DataProcessing/Template/DataProcGallery.rst.txt

..  rubric:: Output

The array now contains the images ordered in rows and columns. For each image
there is a desired width and height supplied.

..  figure:: /Images/ManualScreenshots/FrontendOutput/DataProcessing/GalleryProcessor.png
    :class: with-shadow
    :alt: Gallery dump and output
