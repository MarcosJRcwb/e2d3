<template lang="jade">
.modal.fade(tabindex='-1')
  .modal-dialog
    .modal-content
      .modal-header
        h5.modal-title Share your chart!
      .modal-body
        .form-group
          label Share URL
          .input-group
            input.form-control(type='text', v-model='url', @click='select', v-el:url, readonly)
            .input-group-btn
              button.btn.btn-default(@click='copy')
                i.fa.fa-copy
              button.btn.btn-default(@click='share(facebook)')
                i.fa.fa-facebook
              button.btn.btn-default(@click='share(twitter)')
                i.fa.fa-twitter
        .form-group
          label For blog
          textarea.form-control(rows='3', v-model='frame', @click='select', readonly)
      .modal-footer
        button.btn.btn-sm.btn-default(data-dismiss='modal') Close
</template>

<script lang="coffee">
$ = require 'jquery'

module.exports =
  data: () ->
    url: 'http://'

  computed:
    facebook: () ->
      """https://www.facebook.com/sharer/sharer.php?u=#{@url}"""
    twitter: () ->
      """https://twitter.com/home?status=#{@url}"""
    frame: () ->
      """<iframe src="#{@url}" width="100%" height="400" frameborder="0" scrolling="no"></iframe>"""

  methods:
    show: (url) ->
      @url = url
      $(@$el).modal()

    select: (e) ->
      e.preventDefault()
      e.target.select()

    copy: (e) ->
      @$els.url.select()
      document.execCommand('copy') if document.queryCommandSupported('copy')

    share: (url) ->
      window.open(url, 'share', 'width=600,height=258')
</script>
