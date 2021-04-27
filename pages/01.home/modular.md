---
title: reuse.city
menu: Home
form:
    name: my-contact-form
    action: /home
    fields:
        -
            name: email
            id: email
            classes: 'form-control form-control-lg'
            label: Email
            placeholder: 'Email address (required)'
            type: text
            validate:
                rule: email
                required: true
        -
            subscribe: null
            type: checkbox
            label: 'I agree to receive email updates about this co-design lab (optional).'
            validate: null
            required: false
        -
            name: name
            id: name
            label: Name
            classes: 'form-control form-control-lg'
            placeholder: 'Name (optional)'
            autocomplete: 'on'
            type: text
            validate:
                required: false
        -
            name: message
            label: Message
            classes: 'form-control form-control-lg'
            size: long
            placeholder: 'Message (optional)'
            type: textarea
            validate:
                required: false
    buttons:
        -
            type: submit
            value: Submit
            class: 'btn btn-primary btn-block'
        -
            g-recaptcha-response: null
            type: captcha
            label: Captcha
    process:
        -
            email:
                from: '{{ config.plugins.email.from }}'
                to:
                    - '{{ config.plugins.email.from }}'
                    - '{{ form.value.email }}'
                subject: '[Feedback] {{ form.value.name|e }}'
                body: '{% include ''forms/data.html.twig'' %}'
        -
            save:
                fileprefix: feedback-
                dateformat: Ymd-His-u
                extension: txt
                body: '{% include ''forms/data.txt.twig'' %}'
        -
            message: 'Thank you for your message.'
        -
            display: thankyou
onpage_menu: true
content:
    items: '@self.modular'
    order:
        by: default
        dir: asc
        custom:
            - _intro
            - _features
            - _video
            - _pricing
            - _testimonials
            - _text
            - _news
            - _contact
---

