.. _Drag and Drop:

##########################
拖放问题
##########################

在拖放的问题中，学生通过拖动文本或对象到图像的特定位置上来对问题作出回答。

.. image:: ../../../shared/building_and_running_chapters/Images/DragAndDropProblem.png
 :alt: Image of a drag and drop problem

*********************************
创建一个拖放问题
*********************************

要创建一个简单的拖放问题，让学生拖动标签到图像，你需要上传一个图片来让学生在其上拖动标签，之后再创建问题组件。

#. 在 **文件和上传** 页面, 上传你的图片文件。 有关上传文件的详细信息，请参阅 :ref:`Add Files to a Course` 。
#. 在您要创建问题的单元，点击 **添加新的组件** 中的 **问题** , 然后再点击 **高级** 选项卡。
#. 点击 **拖放** 。
#. 点击出现组件中的 **编辑** 。
#. 用你自己的文本替换组件编辑器中的样例文本。
#. 用你上传到 **文件和上传** 页面图片的URL来替换``<drag_and_drop_input>`` 标记中的 **https://studio.edx.org/c4x/edX/DemoX/asset/L9_buckets.png** (例如： **/static/Image.png**)。
#. 对至少一个 ``<draggable>`` 标记，用你希望学生拖动标签中的文字内容来替换 **label** 属性的中的文本。 例如，如果你想让学生单词“Iceland”拖放到您图像上，则新的标签将类似于以下内容：
   
   ``<draggable id="1" label="Iceland"/>``

8. 重复上一步直到你设置完了所有需要的标签。 确保每一个``<draggable>`` 标记的 **id** 属性的值都是不同的。
#. 确定图像上的正确区域的坐标和半径。
#. 在 ``correct_answer = {``中, 以下面的格式为每个标签添加条目。 这些值以像素为单位：

    ``'id':    [[x coordinate, y coordinate], radius]``

    例如,如果你的图片是600像素宽，400像素高， 你希望你的学生到冰岛的标签拖动到一个区域在图像的左上部分，拖动一个瑞典标签靠近图像的右下角部分，该代码将类似于以下 (其中2是瑞典标签的ID):

    .. code-block:: xml

        correct-answer = {
                '1':    [[50, 50], 75]
                '2':    [[550, 350], 75]}

    .. note:: 确保代码包含右大括号 (**}**) 。 
#. 点击 **保存** 。

==========================================
简单拖放问题的代码
==========================================

要创建出现上面图片中的拖放问题，你需要从edX上下载两个文件，并将这些文件上传到 **文件和上传** 的页面中, 然后添加这个问题的代码到一个问题组件中去。

#. 从 edX 上下载这些文件:

  * Allopurinol.gif
  * AllopurinolAnswer.gif

  点击 http://files.edx.org/DragAndDropProblemFiles.zip 下载包含这两个文件的压缩包。

2. 上传 Allopurinol.gif 和 AllopurinolAnswer.gif 这两个文件到 **文件和上传** 页面。
#. 在你想要添加问题的位置，点击 **添加新的组件** 中的 **问题**  然后再点击 **高级** 选项卡 。
#. 点击 **拖放** 。
#. 点击出现组件中的 **编辑** 。
#. 在组件编辑器中用下面的代码替换示例代码。
#. 点击 **保存** 。

**问题的代码**:

.. code-block:: xml

  <problem>
    <p> Allopurinol is a drug used to treat and prevent gout, a very painful form of arthritis. Once only a “rich man’s disease”, gout has become more and more common in recent decades – affecting about 3 million people in the United States alone. Deposits of needle-like crystals of uric acid in connective tissue or joint spaces cause the symptoms of swelling, stiffness and intense pain. Individuals with gout overproduce uric acid because they cannot eliminate it efficiently. Allopurinol treats and prevents gout by stopping the overproduction of uric acid through inhibition of an enzyme required for the synthesis of uric acid. </p>
    <p> You are shown one of many possible molecules. On the structure of allopurinol below, identify the functional groups that are present by dragging the functional group name listed onto the appropriate target boxes on the structure. If you want to change an answer, you have to drag off the name as well. You may need to scroll through the names of functional groups to see all options. </p>
    <customresponse>
      <drag_and_drop_input no_labels="true" one_per_target="true" target_outline="true" img="/static/Allopurinol.gif">
        <draggable can_reuse="true" label="methyl" id="1"/>
        <draggable can_reuse="true" label="hydroxyl" id="2"/>
        <draggable can_reuse="true" label="amino" id="3"/>
        <draggable can_reuse="true" label="carboxyl" id="4"/>
        <draggable can_reuse="true" label="aldehyde" id="5"/>
        <draggable can_reuse="true" label="phosphate" id="6"/>
        <draggable can_reuse="true" label="sulfhydryl" id="7"/>
        <draggable can_reuse="true" label="phenyl" id="8"/>
        <draggable can_reuse="true" label="none" id="none"/>
        <target id="0" h="53" w="66" y="55.100006103515625" x="131.5"/>
        <target id="1" h="113" w="55" y="140.10000610351562" x="181.5"/>
      </drag_and_drop_input>
      <answer type="loncapa/python"> 
  correct_answer = [ {'draggables': ['2'], 'targets': ['0' ], 'rule':'unordered_equal' }, 
  {'draggables': ['none'], 'targets': ['1' ], 'rule':'unordered_equal' }] 
  if draganddrop.grade(submission[0], correct_answer): 
      correct = ['correct'] 
  else: 
      correct = ['incorrect'] 
      </answer>
    </customresponse>
    <solution>
      <img src="/static/AllopurinolAnswer.gif"/>
    </solution>
  </problem>


.. _Drag and Drop Problem XML:

*********************************
拖放问题的XML
*********************************

.. code-block:: xml

    <problem>
        Here's an example of a "Drag and Drop" question set. Click and drag each word in the scrollbar below, up to the numbered bucket which matches the number of letters in the word.
        <customresponse>
            <drag_and_drop_input img="https://studio.edx.org/c4x/edX/DemoX/asset/L9_buckets.png">
                <draggable id="1" label="a"/>
                <draggable id="2" label="cat"/>
                <draggable id="3" label="there"/>
                <draggable id="4" label="pear"/>
                <draggable id="5" label="kitty"/>
                <draggable id="6" label="in"/>
                <draggable id="7" label="them"/>
                <draggable id="8" label="za"/>
                <draggable id="9" label="dog"/>
                <draggable id="10" label="slate"/>
                <draggable id="11" label="few"/>
            </drag_and_drop_input>
            <answer type="loncapa/python">
               correct_answer = {
                   '1':      [[70, 150], 121],
                   '6':      [[190, 150], 121],
                   '8':      [[190, 150], 121],
                   '2':      [[310, 150], 121],
                   '9':      [[310, 150], 121],
                   '11':     [[310, 150], 121],
                   '4':      [[420, 150], 121],
                   '7':      [[420, 150], 121],
                   '3':      [[550, 150], 121],
                   '5':      [[550, 150], 121],
                   '10':     [[550, 150], 121]}
                   if draganddrop.grade(submission[0], correct_answer):
                       correct = ['correct']
                   else:
                       correct = ['incorrect']
            </answer>
        </customresponse>
        <customresponse>
            <text>
                <h2>Drag and Drop with Outline</h2>
                <p>Please label hydrogen  atoms connected with left carbon atom.</p>
            </text>
            <drag_and_drop_input img="https://studio.edx.org/c4x/edX/DemoX/asset/ethglycol.jpg" target_outline="true" one_per_target="true" no_labels="true" label_bg_color="rgb(222, 139, 238)">
                <draggable id="1" label="Hydrogen" />
                <draggable id="2" label="Hydrogen" />
                <target id="t1_o" x="10" y="67" w="100" h="100"/>
                <target id="t2" x="133" y="3" w="70" h="70"/>
                <target id="t3" x="2" y="384" w="70" h="70"/>
                <target id="t4" x="95" y="386" w="70" h="70"/>
                <target id="t5_c" x="94" y="293" w="91" h="91"/>
                <target id="t6_c" x="328" y="294" w="91" h="91"/>
                <target id="t7" x="393" y="463" w="70" h="70"/>
                <target id="t8" x="344" y="214" w="70" h="70"/>
                <target id="t9_o" x="445" y="162" w="100" h="100"/>
                <target id="t10" x="591" y="132" w="70" h="70"/>
            </drag_and_drop_input>
            <answer type="loncapa/python">
                correct_answer = [{
                    'draggables': ['1', '2'],
                    'targets': ['t2', 't3', 't4' ],
                    'rule':'anyof'
                }]
                if draganddrop.grade(submission[0], correct_answer):
                    correct = ['correct']
                else:
                    correct = ['incorrect']
            </answer>
        </customresponse>
    </problem>


========
标记
========

* ``<customresponse>``: 表示该问题是一个自定义回答问题。

* ``<drag_and_drop_input>``: 表示自定义回答问题是一个拖放问题。

* ``<draggable>``: 指定学生将拖到基础图像中的一个对象。

* ``<target>``: 指定拖拽元素在基本图片上所要放置的位置。

**标记:** ``<drag_and_drop_input>``

  属性

  .. list-table::
     :widths: 20 80
     :header-rows: 1

     * - 属性
       - 说明
     * - img (必要的)
       - 将成为基本图像的图片的相对路径。 所有的拖拽元素可以拖动到它。
     * - target_outline 
       - 指定 目标周围 (如果指定了它们) 是否画出轮廓线 (灰色虚线)。 它的值可以是'true' 或者 'false'。
         如果没有指定则目标没有轮廓线。
     * - one_per_target 
       - 指定是否允许多余于一个拖拽元素被放置在同一个目标中。 的值可以是'true' 或者 'false'。
         如果没有指定，默认值是 'true'.
     * - no_labels (必要的)
       - 默认值是 false 。 默认行为中，如果标签没有设置，标签从ID获得。 如果 no_labels 设置为 true ，那么标签不会自动由ID生成，一个不能设置标签，将获得唯一的图标。

  子标记

     * ``<draggable>``
     * ``<target>``

**标记:** ``<draggable>``

指定拖放问题中的一个拖拽元素。

拖拽元素是用户必须拖出滑块并拖放到基本图像上。 完成拖动操作后，如果拖拽元素的中心位于图像矩形区域之外，它将被退回滑块中去。

为了便于评分，每个拖拽元素都要有唯一的ID。

  属性

  .. list-table::
     :widths: 20 80
     :header-rows: 1

     * - 属性
       - 说明
     * - id (必须的)
       - 拖拽元素唯一的标识。
     * - label (可选的)
       - 用户可以看到的文本标签。
     * - icon (可选的)
       - 当拖拽元素是图片时，图片文件的相对路径。
     * - can_reuse
       - 默认情况下为false。 如果设置为true，则同一个拖拽元素可以使用多次。

  子标记
  
  (无)

**标记:** ``<target>``

指定基本图片上学生必须放置拖拽元素的位置。 按照设计如果拖拽元素的中心在目标区域之内，即在由 [[x, y], [x + w, y + h]] 所指定的矩形区域内，则该元素在目标区域内。
否则就在目标区域之外。

如果你至少指定了一个目标，当学生将拖拽元素拖放到目标之外时，拖拽元素会被退回到滑块中。

如果你没有指定目标区域，学生可以把拖拽元素放到基本图片上的任何位置。

  属性

  .. list-table::
     :widths: 20 80
     :header-rows: 1

     * - 属性
       - 说明
     * - id (必须的)
       - 拖拽元素唯一的标识。
     * - x
       - 目标区域的左上角将定位在基本图像上的X坐标。
     * - y
       - 目标区域的左上角将定位在基本图像上的Y坐标。
     * - w
       - 目标区域的宽度，以像素为单位。
     * - h
       - 目标区域的高度，以像素为单位。

  子标记

  (无)

**********************
Targets on Draggables
**********************

Sometimes it is not enough to have targets only on the base image, and all of
the draggables on these targets. If a complex problem exists where a draggable
must become itself a target (or many targets), then the following extended
syntax can be used.

::

    ...
    <draggable {attribute list}>
        <target {attribute list} />
        <target {attribute list} />
        <target {attribute list} />
        ...
    </draggable>
    ...

The attribute list in the tags above (``draggable`` and ``target``) is the same
as for normal ``draggable`` and ``target`` tags. The only difference is when
you will be specifying inner target position coordinates. Use the ``x`` and
``y`` attributes to set the offset of the inner target from the upper-left
corner of the parent draggable (that contains the inner target).

=====================================
Limitations of targets on draggables
=====================================

* Currently there is a limitation to the level of nesting of targets.

  Even though you can pile up a large number of draggables on targets that
  themselves are on draggables, the Drag and Drop problem will be graded only
  if there is a maximum of two levels of targets. The first level are the
  `base` targets. They are attached to the base image. The second level are the
  targets defined on draggables.

* Another limitation is that the target bounds are not checked against other
  targets.

  You must make sure that there is no overlapping of targets. You should also
  ensure that targets on draggables are smaller than the actual parent
  draggable. Technically this is not necessary, but from the usability
  perspective it is desirable.

* You can have targets on draggables only in the case when there are base
  targets defined (base targets are attached to the base image).

  If you do not have base targets, then you can only have a single level of
  nesting (draggables on the base image). In this case the client side will be
  reporting (x,y) positions of each draggable on the base image.

**********************
Correct answer format
**********************

For specifying answers for targets on draggables, see `Answer format for
targets on draggables`_.

There are two correct answer formats: short and long.

In short form, the correct answer is mapping of ``draggable_id`` to
``target_id``::

    correct_answer = {'grass':     [[300, 200], 200], 'ant': [[500, 0], 200]}
    correct_answer = {'name4': 't1', '7': 't2'}

In long form, the correct answer is list of dicts. Every dict has 3 keys:
``draggables``, ``targets`` and ``rule``. For example::

    correct_answer = [
    {
      'draggables':   ['7', '8'],
      'targets':  ['t5_c', 't6_c'],
      'rule': 'anyof'
    },
    {
      'draggables': ['1', '2'],
      'targets': ['t2_h', 't3_h', 't4_h', 't7_h', 't8_h', 't10_h'],
      'rule': 'anyof'
    }]

"Draggables" is the list of draggable IDs. "Target" is the list of target IDs
that draggables must be dragged to.

.. Caution::
  Draggables in dicts inside the ``correct_answer`` list must not intersect.

Wrong (for draggable id 7)::

    correct_answer = [
    {
      'draggables':   ['7', '8'],
      'targets':  ['t5_c', 't6_c'],
      'rule': 'anyof'
    },
    {
      'draggables': ['7', '2'],
      'targets': ['t2_h', 't3_h', 't4_h', 't7_h', 't8_h', 't10_h'],
      'rule': 'anyof'
    }]

The values for ``rule`` follow. 

* ``exact``: Targets for draggable IDs in ``user_answer`` are the same as
  targets from the correct answer. For example, for draggables 7 and 8, the
  user must drag 7 to target1 and 8 to target2 if the ``correct_answer`` is::

    correct_answer = [
      {
      'draggables':   ['7', '8'],
      'targets':  ['tartget1', 'target2'],
      'rule': 'exact'
    }]


* ``unordered_equal``: Allows draggables be dragged to targets unordered. For
  students to drag 7 to target1 or target2 and 8 to target2 or target1 and 7
  and 8 must be in different targets, then correct answer must be::

    correct_answer = [
    {
      'draggables':   ['7', '8'],
      'targets':  ['tartget1', 'target2'],
      'rule': 'unordered_equal'
    }]


* ``anyof``: Allows draggables to be dragged to any target. For students to
  drag 7 and 8 to target1 or target2, any of these are correct with the `anyof`
  rule::

    correct_answer = [
    {
      'draggables':   ['7', '8'],
      'targets':  ['tartget1', 'target2'],
      'rule': 'anyof'
    }]

If ``can_reuse`` is true, then you have draggables a,b,c and 10 targets. These
will allow you to drag 4 ``a`` draggables to [``target1``,  ``target4``,
``target7``, ``target10``]; you do not need to write ``a`` four times. Also
this will allow you to drag the ``b`` draggable to target2 or target5 for
target5 and target2.::

    correct_answer = [
        {
          'draggables': ['a'],
          'targets': ['target1',  'target4', 'target7', 'target10'],
          'rule': 'unordered_equal'
        },
        {
          'draggables': ['b'],
          'targets': ['target2', 'target5', 'target8'],
          'rule': 'anyof'
        },
        {
          'draggables': ['c'],
          'targets': ['target3', 'target6', 'target9'],
          'rule': 'unordered_equal'
        }]

Sometimes you want to allow students to drag only two ``b`` draggables. In this
case you should use the ``anyof+number`` or ``unordered_equal+number`` rule::

    correct_answer = [
        {
          'draggables': ['a', 'a', 'a'],
          'targets': ['target1',  'target4', 'target7'],
          'rule': 'unordered_equal+number'
        },
        {
          'draggables': ['b', 'b'],
          'targets': ['target2', 'target5', 'target8'],
          'rule': 'anyof+number'
        },
        {
          'draggables': ['c'],
          'targets': ['target3', 'target6', 'target9'],
          'rule': 'unordered_equal'
        }]

When there are no multiple draggables per targets (one_per_target=``true``),
for the same number of draggables, ``anyof`` is equal to ``unordered_equal``.

If ``can_reuse=true``, then you must use only the long form of the correct
answer.

=======================================
Answer format for targets on draggables
=======================================

As with the cases described above, an answer must provide precise positioning
for each draggable (on which targets it must reside). In the case when a
draggable must be placed on a target that itself is on a draggable, then the
answer must contain the chain of target-draggable-target.

For example, suppose we have three draggables - ``up``, ``s``, and ``p``.
Draggables ``s`` and ``p`` have targets on themselves. More specifically,
``p`` has three targets - ``1``, ``2``, and ``3``. The first requirement is
that ``s`` and ``p`` are positioned on specific targets on the base image. The
second requirement is that draggable ``up`` is positioned on specific targets
of draggable ``p``. Below is an excerpt from a problem::

    <draggable id="up" icon="/static/images/images_list/lcao-mo/up.png" can_reuse="true" />

    <draggable id="s" icon="/static/images/images_list/lcao-mo/orbital_single.png" label="s orbital" can_reuse="true" >
        <target id="1" x="0" y="0" w="32" h="32"/>
    </draggable>

    <draggable id="p" icon="/static/images/images_list/lcao-mo/orbital_triple.png" can_reuse="true" label="p orbital" >
      <target id="1" x="0" y="0" w="32" h="32"/>
      <target id="2" x="34" y="0" w="32" h="32"/>
      <target id="3" x="68" y="0" w="32" h="32"/>
    </draggable>

    ...

    correct_answer = [
        {
          'draggables': ['p'],
          'targets': ['p-left-target', 'p-right-target'],
          'rule': 'unordered_equal'
        },
        {
          'draggables': ['s'],
          'targets': ['s-left-target', 's-right-target'],
          'rule': 'unordered_equal'
        },
        {
          'draggables': ['up'],
          'targets': ['p-left-target[p][1]', 'p-left-target[p][2]', 'p-right-
             target[p][2]', 'p-right-target[p][3]',],
          'rule': 'unordered_equal'
        }
    ]

Note that you must specify rules for all draggables, even if a draggable gets
included in more than one chain.

*************
Grading logic
*************

#. The student's answer and the correct answer are parsed to the same format.
   ::

    group_id: group_draggables, group_targets, group_rule

  ``group_id`` is ordinal number, for every dict in correct answer incremental
  ``group_id`` is assigned: 0, 1, 2, ...

  Draggables from the user answer are added to the same group_id where
  identical draggables from the correct answer are, for example::

    If correct_draggables[group_0] = [t1, t2] then
    user_draggables[group_0] are all draggables t1 and t2 from the user answer:
    [t1] or [t1, t2] or [t1, t2, t2] etc..

2. For every group from the user answer, for that group's draggables, if
   ``number`` is in the group rule, set() is applied. If ``number`` is not in
   rule, set is not applied::

    set() : [t1, t2, t3, t3] -> [t1, t2, ,t3]

  For every group, at this step, draggables lists are equal.

3. For every group, lists of targets are compared using the rule for that
   group.

==========================
Set and ``+number`` cases
==========================

``set()`` and ``+number`` are needed only for the case of reusable draggables.
For other cases there are no equal draggables in list, so set() does nothing.

* The ``set()`` operation allows you to create a rule for the case of "any
  number of the same draggable can be dragged to targets"::

    {
      'draggables': ['draggable_1'],
      'targets': ['target3', 'target6', 'target9'],
      'rule': 'anyof'
    }

* The ``number`` rule is used for the case of reusable draggables, when you
  want to fix number of draggable to drag. In this example only two instances
  of draggables_1 are allowed to be dragged::

    {
      'draggables': ['draggable_1', 'draggable_1'],
      'targets': ['target3', 'target6', 'target9'],
      'rule': 'anyof+number'
    }


* Note, that in using rule ``exact``, one does not need ``number``, because you
  cannot recognize from the user interface which reusable draggable is on which
  target. For example::

    {
      'draggables': ['draggable_1', 'draggable_1', 'draggable_2'],
      'targets': ['target3', 'target6', 'target9'],
      'rule': 'exact'
    }


    Correct handling of this example is to create different rules for
    draggable_1 and draggable_2.

* For ``unordered_equal`` (or ``exact``) you don't need ``number`` if you have
  only the same draggable in the group, as the target length will provide
  the constraint for the number of draggables::

    {
      'draggables': ['draggable_1'],
      'targets': ['target3', 'target6', 'target9'],
      'rule': 'unordered_equal'
    }

  This means that only ``draggable_1`` can be dragged.

* But if you have more than one different reusable draggable in the list, you
  may use the ``number`` rule::

    {
      'draggables': ['draggable_1', 'draggable_1', 'draggable_2'],
      'targets': ['target3', 'target6', 'target9'],
      'rule': 'unordered_equal+number'
    }

If you do not use ``number``, the draggables list will be set to
[``draggable_1``, ``draggable_2``].