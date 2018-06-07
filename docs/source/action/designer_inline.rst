.. _Inline:

Inline Motor Screen
===================

For this screen we will want to present to the user useful information to operate
the motors but also provide a way for them to access other parameters considered
**Expert**. Also, to ensure that we can re-use this screen into other displays,
it will be necessary to use :ref:`Macros` in this screen that will later be
replaced by the proper information depending on each motor.

The finished result will look like this:

.. figure:: /_static/action/inline/inline.png
   :scale: 75 %
   :align: center
   :alt: Inline Motor Screen

   Inline Motor Screen

* **Step 1.**

  Let's start by opening the :ref:`Qt Designer <Designer>`
  and creating a new ``Widget``.

  .. figure:: /_static/action/new_widget.gif
     :scale: 75 %
     :align: center

* **Step 2.**

  With the new form available, let's add a GridLayout widget to it and to make it
  fill the whole form let's select ``Layout Vertically`` for the Form.

  .. figure:: /_static/action/inline/inline_layout.gif
     :scale: 75 %
     :align: center

* **Step 3.**

  Now that we have a layout, let's take a look at the widgets on this screen:

  .. figure:: /_static/action/inline/widgets.png
     :scale: 75 %
     :align: center

  * **Step 3.1.**

    The first ``PyDMLabel`` will display the description of the Motor:

    #. Drag and drop a ``PyDMLabel`` at the previously added ``GridLayout``.
    #. Set the ``Channel`` property of this label to: ``ca://${MOTOR}.DESC``.

       * ${MOTOR} is the macro that will later be replaced by the value sent by screens
         using this widget in embedded displays, related displays or even when launching
         using the command line.

    #. Click at the arrow near to the ``Font`` property and mark the checkbox for ``Bold``.

    .. figure:: /_static/action/inline/inline_desc.gif
       :scale: 75 %
       :align: center

  * **Step 3.2.**

    The second widget is a ``PyDMLineEdit`` which will be used to set the desired
    position for the motor:

    #. Drag and drop a ``PyDMLineEdit`` at the ``GridLayout`` on the side of the
       previously added ``PyDMLabel`` (**Note**: The border will become blue showing that
       the widget will be placed on the side and not on top or under the other widget).
    #. Set the ``Channel`` property of this line edit to: ``ca://${MOTOR}.VAL``.
    #. Change its ``displayFormat`` property to ``Decimal``.
    #. Expand the ``sizePolicy`` property and set ``Horizontal Policy`` and
       ``Vertical Policy`` to ``Fixed``.

       * This will make the widget respect the size on screen.

    #. Expand the ``minimumSize`` property and set ``Width`` to ``75``.

       * This property will indicate the minimum size constrains for the widget and
         avoid this widget to be hidden or reduced to an unusable size on window resizing.

  * **Step 3.3.**

    The third widget is a ``PyDMLabel`` which will be used to monitor the readback
    value for the motor:

    #. Drag and drop a ``PyDMLabel`` at the ``GridLayout`` on the side of the
       previously added ``PyDMLineEdit``.
    #. Set the ``Channel`` property of this line edit to: ``ca://${MOTOR}.RBV``.
    #. Change its ``displayFormat`` property to ``Decimal``.
    #. Expand the ``sizePolicy`` property and set ``Horizontal Policy`` and
       ``Vertical Policy`` to ``Fixed``.

       * This will make the widget respect the size on screen.

    #. Expand the ``minimumSize`` property and set ``Width`` to ``75``.

       * This property will indicate the minimum size constrains for the widget and
         avoid this widget to be hidden or reduced to an unusable size on window resizing.

  * **Step 3.4.**

    The forth widget is a ``PyDMByteIndicator`` which will be used for visual
    feedback that the motor is moving:

    #. Drag and drop a ``PyDMByteIndicator`` at the ``GridLayout`` on the side of the
       previously added ``PyDMLabel``.
    #. Set the ``Channel`` property of this line edit to: ``ca://${MOTOR}.MOVN``.
    #. Turn off the ``showLabels`` property since we are only interested on the
       color for this widget.
    #. Set the ``circles`` property so instead of a square we have a circle.
    #. Expand the ``sizePolicy`` property and set ``Horizontal Policy`` and
       ``Vertical Policy`` to ``Fixed``.

    #. Expand the ``minimumSize`` property and set ``Width`` and ``Height`` to
       ``32``.
    #. Repeat the same previous step for the ``maximumSize`` property.

  * **Step 3.5.**

    The fifth widget is a ``PyDMPushButton`` which will be used to stop the motor:

    #. Drag and drop a ``PyDMPushButton`` at the ``GridLayout`` on the side of the
       previously added ``PyDMByteIndicator``.
    #. Set the ``channel`` property of this line edit to: ``ca://${MOTOR}.STOP``.
    #. Set the ``pressValue`` property to ``1``.

       * This is the value that will be written to the channel once the button is
         pressed.

    #. Set the ``text`` property to ``Stop``.
    #. Expand the ``sizePolicy`` property and set ``Horizontal Policy`` to ``Minimum``
       and the ``Vertical Policy`` to ``Fixed``.
    #. Set the ``styleSheet`` property to ``background-color: red;`` in order to
       give the button a nice look and feel and bring the attention to it in case
       of emergency.

  * **Step 3.6.**

    The sixty widget is also a ``PyDMPushButton`` which will be used to tweak the
    motor a certain distance on the positive direction:

    #. Drag and drop a ``PyDMPushButton`` at the ``GridLayout`` on the side of the
       previously added ``PyDMPushButton``.
    #. Set the ``channel`` property of this line edit to: ``ca://${MOTOR}.VAL``.
    #. Set the ``pressValue`` property to ``10``.
    #. Set the ``relativeCHange`` property so instead of writing the value the
       new value written to the channel will be relative to the current channel
       value.
    #. Set the ``text`` property to ``Tw +10``.

  * **Step 3.7.**

    The seventh widget is also a ``PyDMPushButton`` which will be used to tweak the
    motor a certain distance on the negative direction:

    #. Drag and drop a ``PyDMPushButton`` at the ``GridLayout`` on the side of the
       previously added ``PyDMPushButton``.
    #. Set the ``channel`` property of this line edit to: ``ca://${MOTOR}.VAL``.
    #. Set the ``pressValue`` property to ``-10``.
    #. Set the ``relativeCHange`` property so instead of writting the value the
       new value written to the channel will be relative to the current channel
       value.
    #. Set the ``text`` property to ``Tw -10``.

  * **Step 3.8.**

    The final widget is a ``PyDMRelatedDisplayButton`` which will be used to launch
    the **engineer** screen so users can configure advanced parameters and troubleshoot
    possible issues with the motor:

    #. Drag and drop a ``PyDMRelatedDisplayButton`` at the ``GridLayout`` on the
       side of the previously added ``PyDMPushButton``.
    #. Set the ``text`` property to ``Engineer...``.
    #. Set the ``displayFilename`` property to ``expert_motor.ui``.

       .. note::

          We will create the ``expert_motor.ui`` file on the next section.

    #. Set the ``macros`` property to ``{"MOTOR":"${MOTOR}"}``.

       * This macro will use the received macro ``${MOTOR}`` and retransmit it to
         the new window.

    #. Set the ``openInNewWindow`` property so the screen show up in a standalone
       window.
    #. Expand the ``minimumSize`` property and set ``Width`` to ``125`` and
       ``Height`` to ``24``.
    #. Repeat the same previous step for the ``maximumSize`` property.

  * **Step 3.9.**

    After adding all the widgets to the layout, it will look like this:

    .. figure:: /_static/action/inline/inline_all_widgets.png
       :scale: 50 %
       :align: center

    Let's adjust the sizes and reduce the top and bottom margins on the layout.

    #. Using the Object Inspector on the top-right corner, select the ``gridLayout``
       object and:

       * Set the property ``layoutRightMargin`` to ``5``.
       * Set the property ``layoutBottomMargin`` to ``5``.
       * Set the property ``layoutHorizontalSpacing`` to ``10``.
       * Set the property ``layoutVerticalSpacing`` to ``5``.

    #. Using the Object Inspector on the top-right corner, select the ``Form``
       object and:

       * Expand the ``geometry`` property and set ``Width`` to ``700`` and ``Height`` to
         ``32``.
       * Expand the ``sizePolicy`` property and set ``Vertical Policy`` to ``Fixed``.
       * Expand the ``minimumSize`` property and set ``Width`` to ``700`` and ``Height`` to
         ``32``.
       * Expand the ``maximumSize`` property and set ``Height`` to ``38``.
       * Scroll all the way down on the property editor and set ``layoutLeftMargin``,
         ``layoutTopMargin``, ``layoutRightMargin``, ``layoutBottomMargin`` and
         ``layoutSpacing`` to ``0`` so the form is very tight.

    The end result will be something like this:

    .. figure:: /_static/action/inline/inline_all_widgets_ok.png
       :scale: 100 %
       :align: center

* **Step 4.**

  Save this file as ``inline_motor.ui``.

  .. warning::
     For this tutorial it is important to use this file name as it will be referenced
     at the other sections. If you change it please remember to also change at the
     next steps when referenced.

* **Step 5.**

  Test the Inline Motor Screen:

  .. code-block:: bash

     pydm -m '{"MOTOR":"IOC:m1"}' inline_motor.ui

  .. figure:: /_static/action/inline/inline.png
     :scale: 75 %
     :align: center
     :alt: Inline Motor Screen

.. note::
    You can download this file using :download:`this link </_static/code/inline_motor.ui>`.