- [Project: 30 Demos in 6 Weeks](<./Project_ 30 Demos in 6 Weeks.md>)
    - [x] [Experiment](./Experiment.md) - Demo how it was possible to use the combination of [roam/render](./roam_render.md) and [roam/templates](./roam_templates.md) to create a **factory template** the creates customizable dropdowns which add block-refs to a selected item from a particular list.
        - Video
            - <https://www.loom.com/share/1adf78d01db9435fb69bf4249a296a66>
        - To use 
            - [ ] copy this block into your graph #.bp3-card
## Conor's [Factory Template](<./Factory Template.md>) for creating Option Dropdowns based on block refences  #roam/templates
- Congratulations! You have just created a new **Dropdown Template** 
    - #.rm-g  #.rm-h 
        - [ ] Edit the block below to change the template
            - [RM/Component/Select](./RM_Component_Select.md) an item from [iYpGdGk0B](<./February 10th, 2023.md>) [roam/templates](./roam_templates.md)
                - {{[roam/render](./roam_render.md): ((pBiRi-Hba)) [iYpGdGk0B](<./February 10th, 2023.md>)}}
        - [ ] Edit these blocks to change the items visible in the dropdown
            - Dropdown List
                - A
                - B
                - C
- [ ]  Apply the template #.rm-E 
    - [ ] type `;;`   
    - [ ] search for the label you've given it here [->](((ovqdW0R_j))) 
    -  This will produce a custom Select Component like this one 
        - {{[roam/render](./roam_render.md): ((pBiRi-Hba)) [iYpGdGk0B](<./February 10th, 2023.md>)}} 
        - built off this  [iYpGdGk0B](<./February 10th, 2023.md>)
- This component is an experiment, and was built paritally as a demo of what you can do with  [roam/render](./roam_render.md) - a feature of roam that allows you to build interactive components out of code blocks written *inside* your roam graph and referenced by the component in this format `{{[roam/render](./roam_render.md): ((id for the code block goes here)) }}` 
    - If you'd like to edit the code for the template - you can edit it [here](((pBiRi-Hba)))
```clojure
(ns niki.dropdown
  (:require
    [clojure.string :as str]
    [roam.block :as block]
    [roam.datascript.reactive :as dr]))

(defn replace-with-block-ref [block-uid opts-uid ref-uid]
  (let [before (->> [:block/uid block-uid]
                 (dr/pull [:block/string])
                 (deref)
                 :block/string)
        pattern (re-pattern
                  (str
                    "\\{\\{"
                    "(?:\\[\\[)?roam/render(?:\\]\\])?:" ;; [roam/render](./roam_render.md)
                    "\\s*"
                    "\\(\\(([a-zA-Z0-9-]+)\\)\\)"        ;; render code block
                    "\\s*"
                    "\\(\\((" opts-uid ")\\)\\)"         ;; options block
                    "\\s*"
                    "(\\(\\(([a-zA-Z0-9-]+)\\)\\))?"     ;; selected block
                    "\\}\\}"))
        after   (str/replace before pattern
                  (str "{{[roam/render](./roam_render.md): (($1)) (($2)) ((" ref-uid "))}}"))]
    (block/update
      {:block
       {:uid block-uid 
        :string after}})))

(defn view-children-clickable [block-uid opts-uid selected-uid]
  (let [children (->> [:block/uid opts-uid]
                   (dr/pull [{:block/children [:block/uid :block/string]}])
                   deref
                   :block/children)]
    [:select {:id opts-uid
              :on-change #(replace-with-block-ref block-uid opts-uid (-> % .-target .-value))}
     (for [c children]
       [:option
        {:value    (:block/uid c)
         :selected (= (:block/uid c) selected-uid)
         :on-change #(replace-with-block-ref (:block/string c))}
        (:block/string c)])]))

(defn main [{:keys [block-uid]} [_ opts-uid] & [_ selected-uid](roam-page://_ selected-uid)]
  [view-children-clickable block-uid opts-uid selected-uid])
```