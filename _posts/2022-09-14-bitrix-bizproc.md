---
layout: post
title: Bitrix bizproc
category: bitrix php
tags: bitrix bizproc php
---
The following code for manipulating variables in Bitrix business processes

<pre>
  <code class="language-php">
    $rootActivity = $this->GetRootActivity();
    $email = $rootActivity->GetVariable('Email');
    
    $data = (new Questionnaires())->getByMail($email);
    
    if (!empty($data)) {
        
        foreach ($data as $prop => $value) {
            $rootActivity->SetVariable($prop, $value);
        }
    
        $rootActivity->SetVariable('QuestionnaireReceived', true);
    }
  </code>
</pre>