---
layout: post
title: "Twitter Stream Exploration"
date: "2016-03-16 17:35:59 -0600"
tags: notebook english twitter exploration
---
<html>
<head><meta charset="utf-8" />
<title>03 - Twitter stream analysis</title>

<script src="https://cdnjs.cloudflare.com/ajax/libs/require.js/2.1.10/require.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/jquery/2.0.3/jquery.min.js"></script>

<style type="text/css">
/*!
 *  Font Awesome 4.2.0 by @davegandy - http://fontawesome.io - @fontawesome
 *  License - http://fontawesome.io/license (Font: SIL OFL 1.1, CSS: MIT License)
 */@font-face{font-family:'FontAwesome';src:url(../components/font-awesome/fonts/fontawesome-webfont.eot?v=4.2.0);src:url(../components/font-awesome/fonts/fontawesome-webfont.eot?#iefix&v=4.2.0)format('embedded-opentype'),url(../components/font-awesome/fonts/fontawesome-webfont.woff?v=4.2.0)format('woff'),url(../components/font-awesome/fonts/fontawesome-webfont.ttf?v=4.2.0)format('truetype'),url(../components/font-awesome/fonts/fontawesome-webfont.svg?v=4.2.0#fontawesomeregular)format('svg');font-weight:400;font-style:normal}.fa{display:inline-block;font:normal normal normal 14px/1 FontAwesome;font-size:inherit;text-rendering:auto;-webkit-font-smoothing:antialiased;-moz-osx-font-smoothing:grayscale}.fa-lg{font-size:1.33333333em;line-height:.75em;vertical-align:-15%}.fa-2x{font-size:2em}.fa-3x{font-size:3em}.fa-4x{font-size:4em}.fa-5x{font-size:5em}.fa-fw{width:1.28571429em;text-align:center}.fa-ul{padding-left:0;margin-left:2.14285714em;list-style-type:none}.fa-ul>li{position:relative}.fa-li{position:absolute;left:-2.14285714em;width:2.14285714em;top:.14285714em;text-align:center}.fa-li.fa-lg{left:-1.85714286em}.fa-border{padding:.2em .25em .15em;border:.08em solid #eee;border-radius:.1em}.fa.pull-left{margin-right:.3em}.fa.pull-right{margin-left:.3em}.fa-spin{-webkit-animation:fa-spin 2s infinite linear;animation:fa-spin 2s infinite linear}@-webkit-keyframes fa-spin{0%{-webkit-transform:rotate(0);transform:rotate(0)}100%{-webkit-transform:rotate(359deg);transform:rotate(359deg)}}@keyframes fa-spin{0%{-webkit-transform:rotate(0);transform:rotate(0)}100%{-webkit-transform:rotate(359deg);transform:rotate(359deg)}}.fa-rotate-90{filter:progid:DXImageTransform.Microsoft.BasicImage(rotation=1);-webkit-transform:rotate(90deg);-ms-transform:rotate(90deg);transform:rotate(90deg)}.fa-rotate-180{filter:progid:DXImageTransform.Microsoft.BasicImage(rotation=2);-webkit-transform:rotate(180deg);-ms-transform:rotate(180deg);transform:rotate(180deg)}.fa-rotate-270{filter:progid:DXImageTransform.Microsoft.BasicImage(rotation=3);-webkit-transform:rotate(270deg);-ms-transform:rotate(270deg);transform:rotate(270deg)}.fa-flip-horizontal{filter:progid:DXImageTransform.Microsoft.BasicImage(rotation=0, mirror=1);-webkit-transform:scale(-1,1);-ms-transform:scale(-1,1);transform:scale(-1,1)}.fa-flip-vertical{filter:progid:DXImageTransform.Microsoft.BasicImage(rotation=2, mirror=1);-webkit-transform:scale(1,-1);-ms-transform:scale(1,-1);transform:scale(1,-1)}:root .fa-flip-horizontal,:root .fa-flip-vertical,:root .fa-rotate-180,:root .fa-rotate-270,:root .fa-rotate-90{filter:none}.fa-stack{position:relative;display:inline-block;width:2em;height:2em;line-height:2em;vertical-align:middle}.fa-stack-1x,.fa-stack-2x{position:absolute;left:0;width:100%;text-align:center}.fa-stack-1x{line-height:inherit}.fa-stack-2x{font-size:2em}.fa-inverse{color:#fff}.fa-glass:before{content:"\f000"}.fa-music:before{content:"\f001"}.fa-search:before{content:"\f002"}.fa-envelope-o:before{content:"\f003"}.fa-heart:before{content:"\f004"}.fa-star:before{content:"\f005"}.fa-star-o:before{content:"\f006"}.fa-user:before{content:"\f007"}.fa-film:before{content:"\f008"}.fa-th-large:before{content:"\f009"}.fa-th:before{content:"\f00a"}.fa-th-list:before{content:"\f00b"}.fa-check:before{content:"\f00c"}.fa-close:before,.fa-remove:before,.fa-times:before{content:"\f00d"}.fa-search-plus:before{content:"\f00e"}.fa-search-minus:before{content:"\f010"}.fa-power-off:before{content:"\f011"}.fa-signal:before{content:"\f012"}.fa-cog:before,.fa-gear:before{content:"\f013"}.fa-trash-o:before{content:"\f014"}.fa-home:before{content:"\f015"}.fa-file-o:before{content:"\f016"}.fa-clock-o:before{content:"\f017"}.fa-road:before{content:"\f018"}.fa-download:before{content:"\f019"}.fa-arrow-circle-o-down:before{content:"\f01a"}.fa-arrow-circle-o-up:before{content:"\f01b"}.fa-inbox:before{content:"\f01c"}.fa-play-circle-o:before{content:"\f01d"}.fa-repeat:before,.fa-rotate-right:before{content:"\f01e"}.fa-refresh:before{content:"\f021"}.fa-list-alt:before{content:"\f022"}.fa-lock:before{content:"\f023"}.fa-flag:before{content:"\f024"}.fa-headphones:before{content:"\f025"}.fa-volume-off:before{content:"\f026"}.fa-volume-down:before{content:"\f027"}.fa-volume-up:before{content:"\f028"}.fa-qrcode:before{content:"\f029"}.fa-barcode:before{content:"\f02a"}.fa-tag:before{content:"\f02b"}.fa-tags:before{content:"\f02c"}.fa-book:before{content:"\f02d"}.fa-bookmark:before{content:"\f02e"}.fa-print:before{content:"\f02f"}.fa-camera:before{content:"\f030"}.fa-font:before{content:"\f031"}.fa-bold:before{content:"\f032"}.fa-italic:before{content:"\f033"}.fa-text-height:before{content:"\f034"}.fa-text-width:before{content:"\f035"}.fa-align-left:before{content:"\f036"}.fa-align-center:before{content:"\f037"}.fa-align-right:before{content:"\f038"}.fa-align-justify:before{content:"\f039"}.fa-list:before{content:"\f03a"}.fa-dedent:before,.fa-outdent:before{content:"\f03b"}.fa-indent:before{content:"\f03c"}.fa-video-camera:before{content:"\f03d"}.fa-image:before,.fa-photo:before,.fa-picture-o:before{content:"\f03e"}.fa-pencil:before{content:"\f040"}.fa-map-marker:before{content:"\f041"}.fa-adjust:before{content:"\f042"}.fa-tint:before{content:"\f043"}.fa-edit:before,.fa-pencil-square-o:before{content:"\f044"}.fa-share-square-o:before{content:"\f045"}.fa-check-square-o:before{content:"\f046"}.fa-arrows:before{content:"\f047"}.fa-step-backward:before{content:"\f048"}.fa-fast-backward:before{content:"\f049"}.fa-backward:before{content:"\f04a"}.fa-play:before{content:"\f04b"}.fa-pause:before{content:"\f04c"}.fa-stop:before{content:"\f04d"}.fa-forward:before{content:"\f04e"}.fa-fast-forward:before{content:"\f050"}.fa-step-forward:before{content:"\f051"}.fa-eject:before{content:"\f052"}.fa-chevron-left:before{content:"\f053"}.fa-chevron-right:before{content:"\f054"}.fa-plus-circle:before{content:"\f055"}.fa-minus-circle:before{content:"\f056"}.fa-times-circle:before{content:"\f057"}.fa-check-circle:before{content:"\f058"}.fa-question-circle:before{content:"\f059"}.fa-info-circle:before{content:"\f05a"}.fa-crosshairs:before{content:"\f05b"}.fa-times-circle-o:before{content:"\f05c"}.fa-check-circle-o:before{content:"\f05d"}.fa-ban:before{content:"\f05e"}.fa-arrow-left:before{content:"\f060"}.fa-arrow-right:before{content:"\f061"}.fa-arrow-up:before{content:"\f062"}.fa-arrow-down:before{content:"\f063"}.fa-mail-forward:before,.fa-share:before{content:"\f064"}.fa-expand:before{content:"\f065"}.fa-compress:before{content:"\f066"}.fa-plus:before{content:"\f067"}.fa-minus:before{content:"\f068"}.fa-asterisk:before{content:"\f069"}.fa-exclamation-circle:before{content:"\f06a"}.fa-gift:before{content:"\f06b"}.fa-leaf:before{content:"\f06c"}.fa-fire:before{content:"\f06d"}.fa-eye:before{content:"\f06e"}.fa-eye-slash:before{content:"\f070"}.fa-exclamation-triangle:before,.fa-warning:before{content:"\f071"}.fa-plane:before{content:"\f072"}.fa-calendar:before{content:"\f073"}.fa-random:before{content:"\f074"}.fa-comment:before{content:"\f075"}.fa-magnet:before{content:"\f076"}.fa-chevron-up:before{content:"\f077"}.fa-chevron-down:before{content:"\f078"}.fa-retweet:before{content:"\f079"}.fa-shopping-cart:before{content:"\f07a"}.fa-folder:before{content:"\f07b"}.fa-folder-open:before{content:"\f07c"}.fa-arrows-v:before{content:"\f07d"}.fa-arrows-h:before{content:"\f07e"}.fa-bar-chart-o:before,.fa-bar-chart:before{content:"\f080"}.fa-twitter-square:before{content:"\f081"}.fa-facebook-square:before{content:"\f082"}.fa-camera-retro:before{content:"\f083"}.fa-key:before{content:"\f084"}.fa-cogs:before,.fa-gears:before{content:"\f085"}.fa-comments:before{content:"\f086"}.fa-thumbs-o-up:before{content:"\f087"}.fa-thumbs-o-down:before{content:"\f088"}.fa-star-half:before{content:"\f089"}.fa-heart-o:before{content:"\f08a"}.fa-sign-out:before{content:"\f08b"}.fa-linkedin-square:before{content:"\f08c"}.fa-thumb-tack:before{content:"\f08d"}.fa-external-link:before{content:"\f08e"}.fa-sign-in:before{content:"\f090"}.fa-trophy:before{content:"\f091"}.fa-github-square:before{content:"\f092"}.fa-upload:before{content:"\f093"}.fa-lemon-o:before{content:"\f094"}.fa-phone:before{content:"\f095"}.fa-square-o:before{content:"\f096"}.fa-bookmark-o:before{content:"\f097"}.fa-phone-square:before{content:"\f098"}.fa-twitter:before{content:"\f099"}.fa-facebook:before{content:"\f09a"}.fa-github:before{content:"\f09b"}.fa-unlock:before{content:"\f09c"}.fa-credit-card:before{content:"\f09d"}.fa-rss:before{content:"\f09e"}.fa-hdd-o:before{content:"\f0a0"}.fa-bullhorn:before{content:"\f0a1"}.fa-bell:before{content:"\f0f3"}.fa-certificate:before{content:"\f0a3"}.fa-hand-o-right:before{content:"\f0a4"}.fa-hand-o-left:before{content:"\f0a5"}.fa-hand-o-up:before{content:"\f0a6"}.fa-hand-o-down:before{content:"\f0a7"}.fa-arrow-circle-left:before{content:"\f0a8"}.fa-arrow-circle-right:before{content:"\f0a9"}.fa-arrow-circle-up:before{content:"\f0aa"}.fa-arrow-circle-down:before{content:"\f0ab"}.fa-globe:before{content:"\f0ac"}.fa-wrench:before{content:"\f0ad"}.fa-tasks:before{content:"\f0ae"}.fa-filter:before{content:"\f0b0"}.fa-briefcase:before{content:"\f0b1"}.fa-arrows-alt:before{content:"\f0b2"}.fa-group:before,.fa-users:before{content:"\f0c0"}.fa-chain:before,.fa-link:before{content:"\f0c1"}.fa-cloud:before{content:"\f0c2"}.fa-flask:before{content:"\f0c3"}.fa-cut:before,.fa-scissors:before{content:"\f0c4"}.fa-copy:before,.fa-files-o:before{content:"\f0c5"}.fa-paperclip:before{content:"\f0c6"}.fa-floppy-o:before,.fa-save:before{content:"\f0c7"}.fa-square:before{content:"\f0c8"}.fa-bars:before,.fa-navicon:before,.fa-reorder:before{content:"\f0c9"}.fa-list-ul:before{content:"\f0ca"}.fa-list-ol:before{content:"\f0cb"}.fa-strikethrough:before{content:"\f0cc"}.fa-underline:before{content:"\f0cd"}.fa-table:before{content:"\f0ce"}.fa-magic:before{content:"\f0d0"}.fa-truck:before{content:"\f0d1"}.fa-pinterest:before{content:"\f0d2"}.fa-pinterest-square:before{content:"\f0d3"}.fa-google-plus-square:before{content:"\f0d4"}.fa-google-plus:before{content:"\f0d5"}.fa-money:before{content:"\f0d6"}.fa-caret-down:before{content:"\f0d7"}.fa-caret-up:before{content:"\f0d8"}.fa-caret-left:before{content:"\f0d9"}.fa-caret-right:before{content:"\f0da"}.fa-columns:before{content:"\f0db"}.fa-sort:before,.fa-unsorted:before{content:"\f0dc"}.fa-sort-desc:before,.fa-sort-down:before{content:"\f0dd"}.fa-sort-asc:before,.fa-sort-up:before{content:"\f0de"}.fa-envelope:before{content:"\f0e0"}.fa-linkedin:before{content:"\f0e1"}.fa-rotate-left:before,.fa-undo:before{content:"\f0e2"}.fa-gavel:before,.fa-legal:before{content:"\f0e3"}.fa-dashboard:before,.fa-tachometer:before{content:"\f0e4"}.fa-comment-o:before{content:"\f0e5"}.fa-comments-o:before{content:"\f0e6"}.fa-bolt:before,.fa-flash:before{content:"\f0e7"}.fa-sitemap:before{content:"\f0e8"}.fa-umbrella:before{content:"\f0e9"}.fa-clipboard:before,.fa-paste:before{content:"\f0ea"}.fa-lightbulb-o:before{content:"\f0eb"}.fa-exchange:before{content:"\f0ec"}.fa-cloud-download:before{content:"\f0ed"}.fa-cloud-upload:before{content:"\f0ee"}.fa-user-md:before{content:"\f0f0"}.fa-stethoscope:before{content:"\f0f1"}.fa-suitcase:before{content:"\f0f2"}.fa-bell-o:before{content:"\f0a2"}.fa-coffee:before{content:"\f0f4"}.fa-cutlery:before{content:"\f0f5"}.fa-file-text-o:before{content:"\f0f6"}.fa-building-o:before{content:"\f0f7"}.fa-hospital-o:before{content:"\f0f8"}.fa-ambulance:before{content:"\f0f9"}.fa-medkit:before{content:"\f0fa"}.fa-fighter-jet:before{content:"\f0fb"}.fa-beer:before{content:"\f0fc"}.fa-h-square:before{content:"\f0fd"}.fa-plus-square:before{content:"\f0fe"}.fa-angle-double-left:before{content:"\f100"}.fa-angle-double-right:before{content:"\f101"}.fa-angle-double-up:before{content:"\f102"}.fa-angle-double-down:before{content:"\f103"}.fa-angle-left:before{content:"\f104"}.fa-angle-right:before{content:"\f105"}.fa-angle-up:before{content:"\f106"}.fa-angle-down:before{content:"\f107"}.fa-desktop:before{content:"\f108"}.fa-laptop:before{content:"\f109"}.fa-tablet:before{content:"\f10a"}.fa-mobile-phone:before,.fa-mobile:before{content:"\f10b"}.fa-circle-o:before{content:"\f10c"}.fa-quote-left:before{content:"\f10d"}.fa-quote-right:before{content:"\f10e"}.fa-spinner:before{content:"\f110"}.fa-circle:before{content:"\f111"}.fa-mail-reply:before,.fa-reply:before{content:"\f112"}.fa-github-alt:before{content:"\f113"}.fa-folder-o:before{content:"\f114"}.fa-folder-open-o:before{content:"\f115"}.fa-smile-o:before{content:"\f118"}.fa-frown-o:before{content:"\f119"}.fa-meh-o:before{content:"\f11a"}.fa-gamepad:before{content:"\f11b"}.fa-keyboard-o:before{content:"\f11c"}.fa-flag-o:before{content:"\f11d"}.fa-flag-checkered:before{content:"\f11e"}.fa-terminal:before{content:"\f120"}.fa-code:before{content:"\f121"}.fa-mail-reply-all:before,.fa-reply-all:before{content:"\f122"}.fa-star-half-empty:before,.fa-star-half-full:before,.fa-star-half-o:before{content:"\f123"}.fa-location-arrow:before{content:"\f124"}.fa-crop:before{content:"\f125"}.fa-code-fork:before{content:"\f126"}.fa-chain-broken:before,.fa-unlink:before{content:"\f127"}.fa-question:before{content:"\f128"}.fa-info:before{content:"\f129"}.fa-exclamation:before{content:"\f12a"}.fa-superscript:before{content:"\f12b"}.fa-subscript:before{content:"\f12c"}.fa-eraser:before{content:"\f12d"}.fa-puzzle-piece:before{content:"\f12e"}.fa-microphone:before{content:"\f130"}.fa-microphone-slash:before{content:"\f131"}.fa-shield:before{content:"\f132"}.fa-calendar-o:before{content:"\f133"}.fa-fire-extinguisher:before{content:"\f134"}.fa-rocket:before{content:"\f135"}.fa-maxcdn:before{content:"\f136"}.fa-chevron-circle-left:before{content:"\f137"}.fa-chevron-circle-right:before{content:"\f138"}.fa-chevron-circle-up:before{content:"\f139"}.fa-chevron-circle-down:before{content:"\f13a"}.fa-html5:before{content:"\f13b"}.fa-css3:before{content:"\f13c"}.fa-anchor:before{content:"\f13d"}.fa-unlock-alt:before{content:"\f13e"}.fa-bullseye:before{content:"\f140"}.fa-ellipsis-h:before{content:"\f141"}.fa-ellipsis-v:before{content:"\f142"}.fa-rss-square:before{content:"\f143"}.fa-play-circle:before{content:"\f144"}.fa-ticket:before{content:"\f145"}.fa-minus-square:before{content:"\f146"}.fa-minus-square-o:before{content:"\f147"}.fa-level-up:before{content:"\f148"}.fa-level-down:before{content:"\f149"}.fa-check-square:before{content:"\f14a"}.fa-pencil-square:before{content:"\f14b"}.fa-external-link-square:before{content:"\f14c"}.fa-share-square:before{content:"\f14d"}.fa-compass:before{content:"\f14e"}.fa-caret-square-o-down:before,.fa-toggle-down:before{content:"\f150"}.fa-caret-square-o-up:before,.fa-toggle-up:before{content:"\f151"}.fa-caret-square-o-right:before,.fa-toggle-right:before{content:"\f152"}.fa-eur:before,.fa-euro:before{content:"\f153"}.fa-gbp:before{content:"\f154"}.fa-dollar:before,.fa-usd:before{content:"\f155"}.fa-inr:before,.fa-rupee:before{content:"\f156"}.fa-cny:before,.fa-jpy:before,.fa-rmb:before,.fa-yen:before{content:"\f157"}.fa-rouble:before,.fa-rub:before,.fa-ruble:before{content:"\f158"}.fa-krw:before,.fa-won:before{content:"\f159"}.fa-bitcoin:before,.fa-btc:before{content:"\f15a"}.fa-file:before{content:"\f15b"}.fa-file-text:before{content:"\f15c"}.fa-sort-alpha-asc:before{content:"\f15d"}.fa-sort-alpha-desc:before{content:"\f15e"}.fa-sort-amount-asc:before{content:"\f160"}.fa-sort-amount-desc:before{content:"\f161"}.fa-sort-numeric-asc:before{content:"\f162"}.fa-sort-numeric-desc:before{content:"\f163"}.fa-thumbs-up:before{content:"\f164"}.fa-thumbs-down:before{content:"\f165"}.fa-youtube-square:before{content:"\f166"}.fa-youtube:before{content:"\f167"}.fa-xing:before{content:"\f168"}.fa-xing-square:before{content:"\f169"}.fa-youtube-play:before{content:"\f16a"}.fa-dropbox:before{content:"\f16b"}.fa-stack-overflow:before{content:"\f16c"}.fa-instagram:before{content:"\f16d"}.fa-flickr:before{content:"\f16e"}.fa-adn:before{content:"\f170"}.fa-bitbucket:before{content:"\f171"}.fa-bitbucket-square:before{content:"\f172"}.fa-tumblr:before{content:"\f173"}.fa-tumblr-square:before{content:"\f174"}.fa-long-arrow-down:before{content:"\f175"}.fa-long-arrow-up:before{content:"\f176"}.fa-long-arrow-left:before{content:"\f177"}.fa-long-arrow-right:before{content:"\f178"}.fa-apple:before{content:"\f179"}.fa-windows:before{content:"\f17a"}.fa-android:before{content:"\f17b"}.fa-linux:before{content:"\f17c"}.fa-dribbble:before{content:"\f17d"}.fa-skype:before{content:"\f17e"}.fa-foursquare:before{content:"\f180"}.fa-trello:before{content:"\f181"}.fa-female:before{content:"\f182"}.fa-male:before{content:"\f183"}.fa-gittip:before{content:"\f184"}.fa-sun-o:before{content:"\f185"}.fa-moon-o:before{content:"\f186"}.fa-archive:before{content:"\f187"}.fa-bug:before{content:"\f188"}.fa-vk:before{content:"\f189"}.fa-weibo:before{content:"\f18a"}.fa-renren:before{content:"\f18b"}.fa-pagelines:before{content:"\f18c"}.fa-stack-exchange:before{content:"\f18d"}.fa-arrow-circle-o-right:before{content:"\f18e"}.fa-arrow-circle-o-left:before{content:"\f190"}.fa-caret-square-o-left:before,.fa-toggle-left:before{content:"\f191"}.fa-dot-circle-o:before{content:"\f192"}.fa-wheelchair:before{content:"\f193"}.fa-vimeo-square:before{content:"\f194"}.fa-try:before,.fa-turkish-lira:before{content:"\f195"}.fa-plus-square-o:before{content:"\f196"}.fa-space-shuttle:before{content:"\f197"}.fa-slack:before{content:"\f198"}.fa-envelope-square:before{content:"\f199"}.fa-wordpress:before{content:"\f19a"}.fa-openid:before{content:"\f19b"}.fa-bank:before,.fa-institution:before,.fa-university:before{content:"\f19c"}.fa-graduation-cap:before,.fa-mortar-board:before{content:"\f19d"}.fa-yahoo:before{content:"\f19e"}.fa-google:before{content:"\f1a0"}.fa-reddit:before{content:"\f1a1"}.fa-reddit-square:before{content:"\f1a2"}.fa-stumbleupon-circle:before{content:"\f1a3"}.fa-stumbleupon:before{content:"\f1a4"}.fa-delicious:before{content:"\f1a5"}.fa-digg:before{content:"\f1a6"}.fa-pied-piper:before{content:"\f1a7"}.fa-pied-piper-alt:before{content:"\f1a8"}.fa-drupal:before{content:"\f1a9"}.fa-joomla:before{content:"\f1aa"}.fa-language:before{content:"\f1ab"}.fa-fax:before{content:"\f1ac"}.fa-building:before{content:"\f1ad"}.fa-child:before{content:"\f1ae"}.fa-paw:before{content:"\f1b0"}.fa-spoon:before{content:"\f1b1"}.fa-cube:before{content:"\f1b2"}.fa-cubes:before{content:"\f1b3"}.fa-behance:before{content:"\f1b4"}.fa-behance-square:before{content:"\f1b5"}.fa-steam:before{content:"\f1b6"}.fa-steam-square:before{content:"\f1b7"}.fa-recycle:before{content:"\f1b8"}.fa-automobile:before,.fa-car:before{content:"\f1b9"}.fa-cab:before,.fa-taxi:before{content:"\f1ba"}.fa-tree:before{content:"\f1bb"}.fa-spotify:before{content:"\f1bc"}.fa-deviantart:before{content:"\f1bd"}.fa-soundcloud:before{content:"\f1be"}.fa-database:before{content:"\f1c0"}.fa-file-pdf-o:before{content:"\f1c1"}.fa-file-word-o:before{content:"\f1c2"}.fa-file-excel-o:before{content:"\f1c3"}.fa-file-powerpoint-o:before{content:"\f1c4"}.fa-file-image-o:before,.fa-file-photo-o:before,.fa-file-picture-o:before{content:"\f1c5"}.fa-file-archive-o:before,.fa-file-zip-o:before{content:"\f1c6"}.fa-file-audio-o:before,.fa-file-sound-o:before{content:"\f1c7"}.fa-file-movie-o:before,.fa-file-video-o:before{content:"\f1c8"}.fa-file-code-o:before{content:"\f1c9"}.fa-vine:before{content:"\f1ca"}.fa-codepen:before{content:"\f1cb"}.fa-jsfiddle:before{content:"\f1cc"}.fa-life-bouy:before,.fa-life-buoy:before,.fa-life-ring:before,.fa-life-saver:before,.fa-support:before{content:"\f1cd"}.fa-circle-o-notch:before{content:"\f1ce"}.fa-ra:before,.fa-rebel:before{content:"\f1d0"}.fa-empire:before,.fa-ge:before{content:"\f1d1"}.fa-git-square:before{content:"\f1d2"}.fa-git:before{content:"\f1d3"}.fa-hacker-news:before{content:"\f1d4"}.fa-tencent-weibo:before{content:"\f1d5"}.fa-qq:before{content:"\f1d6"}.fa-wechat:before,.fa-weixin:before{content:"\f1d7"}.fa-paper-plane:before,.fa-send:before{content:"\f1d8"}.fa-paper-plane-o:before,.fa-send-o:before{content:"\f1d9"}.fa-history:before{content:"\f1da"}.fa-circle-thin:before{content:"\f1db"}.fa-header:before{content:"\f1dc"}.fa-paragraph:before{content:"\f1dd"}.fa-sliders:before{content:"\f1de"}.fa-share-alt:before{content:"\f1e0"}.fa-share-alt-square:before{content:"\f1e1"}.fa-bomb:before{content:"\f1e2"}.fa-futbol-o:before,.fa-soccer-ball-o:before{content:"\f1e3"}.fa-tty:before{content:"\f1e4"}.fa-binoculars:before{content:"\f1e5"}.fa-plug:before{content:"\f1e6"}.fa-slideshare:before{content:"\f1e7"}.fa-twitch:before{content:"\f1e8"}.fa-yelp:before{content:"\f1e9"}.fa-newspaper-o:before{content:"\f1ea"}.fa-wifi:before{content:"\f1eb"}.fa-calculator:before{content:"\f1ec"}.fa-paypal:before{content:"\f1ed"}.fa-google-wallet:before{content:"\f1ee"}.fa-cc-visa:before{content:"\f1f0"}.fa-cc-mastercard:before{content:"\f1f1"}.fa-cc-discover:before{content:"\f1f2"}.fa-cc-amex:before{content:"\f1f3"}.fa-cc-paypal:before{content:"\f1f4"}.fa-cc-stripe:before{content:"\f1f5"}.fa-bell-slash:before{content:"\f1f6"}.fa-bell-slash-o:before{content:"\f1f7"}.fa-trash:before{content:"\f1f8"}.fa-copyright:before{content:"\f1f9"}.fa-at:before{content:"\f1fa"}.fa-eyedropper:before{content:"\f1fb"}.fa-paint-brush:before{content:"\f1fc"}.fa-birthday-cake:before{content:"\f1fd"}.fa-area-chart:before{content:"\f1fe"}.fa-pie-chart:before{content:"\f200"}.fa-line-chart:before{content:"\f201"}.fa-lastfm:before{content:"\f202"}.fa-lastfm-square:before{content:"\f203"}.fa-toggle-off:before{content:"\f204"}.fa-toggle-on:before{content:"\f205"}.fa-bicycle:before{content:"\f206"}.fa-bus:before{content:"\f207"}.fa-ioxhost:before{content:"\f208"}.fa-angellist:before{content:"\f209"}.fa-cc:before{content:"\f20a"}.fa-ils:before,.fa-shekel:before,.fa-sheqel:before{content:"\f20b"}.fa-meanpath:before{content:"\f20c"}/*!
*
* IPython base
*
*/.modal.fade .modal-dialog{-webkit-transform:translate(0,0);-ms-transform:translate(0,0);-o-transform:translate(0,0);transform:translate(0,0)}code{color:#000}pre{font-size:inherit;line-height:inherit}label{font-weight:400}.border-box-sizing{box-sizing:border-box;-moz-box-sizing:border-box;-webkit-box-sizing:border-box}.corner-all{border-radius:2px}.no-padding{padding:0}.hbox{display:-webkit-box;-webkit-box-orient:horizontal;display:-moz-box;-moz-box-orient:horizontal;display:box;box-orient:horizontal;box-align:stretch;display:flex;flex-direction:row;align-items:stretch}.hbox>*{-webkit-box-flex:0;-moz-box-flex:0;box-flex:0;flex:none}.vbox{display:-webkit-box;-webkit-box-orient:vertical;display:-moz-box;-moz-box-orient:vertical;display:box;box-orient:vertical;box-align:stretch;display:flex;flex-direction:column;align-items:stretch}.vbox>*{-webkit-box-flex:0;-moz-box-flex:0;box-flex:0;flex:none}.hbox.reverse,.reverse,.vbox.reverse{-webkit-box-direction:reverse;-moz-box-direction:reverse;box-direction:reverse;flex-direction:row-reverse}.box-flex0,.hbox.box-flex0,.vbox.box-flex0{-webkit-box-flex:0;-moz-box-flex:0;box-flex:0;flex:none;width:auto}.box-flex1,.hbox.box-flex1,.vbox.box-flex1{-webkit-box-flex:1;-moz-box-flex:1;box-flex:1;flex:1}.box-flex,.hbox.box-flex,.vbox.box-flex{-webkit-box-flex:1;-moz-box-flex:1;box-flex:1;flex:1}.box-flex2,.hbox.box-flex2,.vbox.box-flex2{-webkit-box-flex:2;-moz-box-flex:2;box-flex:2;flex:2}.box-group1{-webkit-box-flex-group:1;-moz-box-flex-group:1;box-flex-group:1}.box-group2{-webkit-box-flex-group:2;-moz-box-flex-group:2;box-flex-group:2}.hbox.start,.start,.vbox.start{-webkit-box-pack:start;-moz-box-pack:start;box-pack:start;justify-content:flex-start}.end,.hbox.end,.vbox.end{-webkit-box-pack:end;-moz-box-pack:end;box-pack:end;justify-content:flex-end}.center,.hbox.center,.vbox.center{-webkit-box-pack:center;-moz-box-pack:center;box-pack:center;justify-content:center}.baseline,.hbox.baseline,.vbox.baseline{-webkit-box-pack:baseline;-moz-box-pack:baseline;box-pack:baseline;justify-content:baseline}.hbox.stretch,.stretch,.vbox.stretch{-webkit-box-pack:stretch;-moz-box-pack:stretch;box-pack:stretch;justify-content:stretch}.align-start,.hbox.align-start,.vbox.align-start{-webkit-box-align:start;-moz-box-align:start;box-align:start;align-items:flex-start}.align-end,.hbox.align-end,.vbox.align-end{-webkit-box-align:end;-moz-box-align:end;box-align:end;align-items:flex-end}.align-center,.hbox.align-center,.vbox.align-center{-webkit-box-align:center;-moz-box-align:center;box-align:center;align-items:center}.align-baseline,.hbox.align-baseline,.vbox.align-baseline{-webkit-box-align:baseline;-moz-box-align:baseline;box-align:baseline;align-items:baseline}.align-stretch,.hbox.align-stretch,.vbox.align-stretch{-webkit-box-align:stretch;-moz-box-align:stretch;box-align:stretch;align-items:stretch}div.error{margin:2em;text-align:center}div.error>h1{font-size:500%;line-height:normal}div.error>p{font-size:200%;line-height:normal}div.traceback-wrapper{text-align:left;max-width:800px;margin:auto}body{position:absolute;left:0;right:0;top:0;bottom:0;overflow:visible}#header{display:none;background-color:#fff;position:relative;z-index:100}#header #header-container{padding-bottom:5px;padding-top:5px;box-sizing:border-box;-moz-box-sizing:border-box;-webkit-box-sizing:border-box}#header .header-bar{width:100%;height:1px;background:#e7e7e7;margin-bottom:-1px}#header-spacer{width:100%;visibility:hidden}@media print{#header{display:none!important}#header-spacer{display:none}}#ipython_notebook{padding-left:0;padding-top:1px;padding-bottom:1px}@media (max-width:991px){#ipython_notebook{margin-left:10px}}#noscript{width:auto;padding-top:16px;padding-bottom:16px;text-align:center;font-size:22px;color:red;font-weight:700}#ipython_notebook img{height:28px}#site{width:100%;display:none;box-sizing:border-box;-moz-box-sizing:border-box;-webkit-box-sizing:border-box;overflow:auto}@media print{#site{height:auto!important}}.ui-button .ui-button-text{padding:.2em .8em;font-size:77%}input.ui-button{padding:.3em .9em}span#login_widget{float:right}#logout,span#login_widget>.button{color:#333;background-color:#fff;border-color:#ccc}#logout.active,#logout.focus,#logout:active,#logout:focus,#logout:hover,.open>.dropdown-toggle#logout,.open>.dropdown-togglespan#login_widget>.button,span#login_widget>.button.active,span#login_widget>.button.focus,span#login_widget>.button:active,span#login_widget>.button:focus,span#login_widget>.button:hover{color:#333;background-color:#e6e6e6;border-color:#adadad}#logout.active,#logout:active,.open>.dropdown-toggle#logout,.open>.dropdown-togglespan#login_widget>.button,span#login_widget>.button.active,span#login_widget>.button:active{background-image:none}#logout.disabled,#logout.disabled.active,#logout.disabled.focus,#logout.disabled:active,#logout.disabled:focus,#logout.disabled:hover,#logout[disabled],#logout[disabled].active,#logout[disabled].focus,#logout[disabled]:active,#logout[disabled]:focus,#logout[disabled]:hover,fieldset[disabled] #logout,fieldset[disabled] #logout.active,fieldset[disabled] #logout.focus,fieldset[disabled] #logout:active,fieldset[disabled] #logout:focus,fieldset[disabled] #logout:hover,fieldset[disabled] span#login_widget>.button,fieldset[disabled] span#login_widget>.button.active,fieldset[disabled] span#login_widget>.button.focus,fieldset[disabled] span#login_widget>.button:active,fieldset[disabled] span#login_widget>.button:focus,fieldset[disabled] span#login_widget>.button:hover,span#login_widget>.button.disabled,span#login_widget>.button.disabled.active,span#login_widget>.button.disabled.focus,span#login_widget>.button.disabled:active,span#login_widget>.button.disabled:focus,span#login_widget>.button.disabled:hover,span#login_widget>.button[disabled],span#login_widget>.button[disabled].active,span#login_widget>.button[disabled].focus,span#login_widget>.button[disabled]:active,span#login_widget>.button[disabled]:focus,span#login_widget>.button[disabled]:hover{background-color:#fff;border-color:#ccc}#logout .badge,span#login_widget>.button .badge{color:#fff;background-color:#333}.nav-header{text-transform:none}#header>span{margin-top:10px}.modal_stretch .modal-dialog{display:-webkit-box;-webkit-box-orient:vertical;display:-moz-box;-moz-box-orient:vertical;display:box;box-orient:vertical;box-align:stretch;display:flex;flex-direction:column;align-items:stretch;min-height:80vh}.modal_stretch .modal-dialog .modal-body{max-height:calc(100vh - 200px);overflow:auto;flex:1}@media (min-width:768px){.modal .modal-dialog{width:700px}select.form-control{margin-left:12px;margin-right:12px}}/*!
*
* IPython auth
*
*/.center-nav{display:inline-block;margin-bottom:-4px}/*!
*
* IPython tree view
*
*/.alternate_upload{background-color:none;display:inline}.alternate_upload.form{padding:0;margin:0}.alternate_upload input.fileinput{text-align:center;vertical-align:middle;display:inline;opacity:0;z-index:2;width:12ex;margin-right:-12ex}.alternate_upload .btn-upload{height:22px}ul#tabs{margin-bottom:4px}ul#tabs a{padding-top:6px;padding-bottom:4px}ul.breadcrumb a:focus,ul.breadcrumb a:hover{text-decoration:none}ul.breadcrumb i.icon-home{font-size:16px;margin-right:4px}ul.breadcrumb span{color:#5e5e5e}.list_toolbar{padding:4px 0;vertical-align:middle}.list_toolbar .tree-buttons{padding-top:1px}.dynamic-buttons{padding-top:3px;display:inline-block}.list_toolbar [class*=span]{min-height:24px}.list_header{font-weight:700;background-color:#eee}.list_placeholder{font-weight:700;padding:4px 7px}.list_container{margin-top:4px;margin-bottom:20px;border:1px solid #ddd;border-radius:2px}.list_container>div{border-bottom:1px solid #ddd}.list_container>div:hover .list-item{background-color:red}.list_container>div:last-child{border:none}.list_item:hover .list_item{background-color:#ddd}.list_item a{text-decoration:none}.list_item:hover{background-color:#fafafa}.action_col{text-align:right}.list_header>div,.list_item>div{line-height:22px;padding:4px 7px}.list_header>div input,.list_item>div input{margin-right:7px;margin-left:14px;vertical-align:baseline;line-height:22px;position:relative;top:-1px}.list_header>div .item_link,.list_item>div .item_link{margin-left:-1px;vertical-align:baseline;line-height:22px}.new-file input[type=checkbox]{visibility:hidden}.item_name{line-height:22px;height:24px}.item_icon{font-size:14px;color:#5e5e5e;margin-right:7px;margin-left:7px;line-height:22px;vertical-align:baseline}.item_buttons{line-height:1em;margin-left:-5px}.item_buttons .btn-group,.item_buttons .input-group{float:left}.item_buttons>.btn,.item_buttons>.btn-group,.item_buttons>.input-group{margin-left:5px}.item_buttons .btn{min-width:13ex}.item_buttons .running-indicator{padding-top:4px;color:#5cb85c}.toolbar_info{height:24px;line-height:24px}input.engine_num_input,input.nbname_input{padding-top:3px;padding-bottom:3px;height:22px;line-height:14px;margin:0}input.engine_num_input{width:60px}.highlight_text{color:#00f}#project_name{display:inline-block;padding-left:7px;margin-left:-2px}#project_name>.breadcrumb{padding:0;margin-bottom:0;background-color:transparent;font-weight:700}#tree-selector{padding-right:0}#button-select-all{min-width:50px}#select-all{margin-left:7px;margin-right:2px}.menu_icon{margin-right:2px}.tab-content .row{margin-left:0;margin-right:0}.folder_icon:before{display:inline-block;font:normal normal normal 14px/1 FontAwesome;font-size:inherit;text-rendering:auto;-webkit-font-smoothing:antialiased;-moz-osx-font-smoothing:grayscale;content:"\f114"}.folder_icon:before.pull-left{margin-right:.3em}.folder_icon:before.pull-right{margin-left:.3em}.notebook_icon:before{display:inline-block;font:normal normal normal 14px/1 FontAwesome;font-size:inherit;text-rendering:auto;-webkit-font-smoothing:antialiased;-moz-osx-font-smoothing:grayscale;content:"\f02d";position:relative;top:-1px}.notebook_icon:before.pull-left{margin-right:.3em}.notebook_icon:before.pull-right{margin-left:.3em}.running_notebook_icon:before{display:inline-block;font:normal normal normal 14px/1 FontAwesome;font-size:inherit;text-rendering:auto;-webkit-font-smoothing:antialiased;-moz-osx-font-smoothing:grayscale;content:"\f02d";position:relative;top:-1px;color:#5cb85c}.running_notebook_icon:before.pull-left{margin-right:.3em}.running_notebook_icon:before.pull-right{margin-left:.3em}.file_icon:before{display:inline-block;font:normal normal normal 14px/1 FontAwesome;font-size:inherit;text-rendering:auto;-webkit-font-smoothing:antialiased;-moz-osx-font-smoothing:grayscale;content:"\f016";position:relative;top:-2px}.file_icon:before.pull-left{margin-right:.3em}.file_icon:before.pull-right{margin-left:.3em}#notebook_toolbar .pull-right{padding-top:0;margin-right:-1px}ul#new-menu{left:auto;right:0}.kernel-menu-icon{padding-right:12px;width:24px;content:"\f096"}.kernel-menu-icon:before{content:"\f096"}.kernel-menu-icon-current:before{content:"\f00c"}#tab_content{padding-top:20px}#running .panel-group .panel{margin-top:3px;margin-bottom:1em}#running .panel-group .panel .panel-heading{background-color:#eee;line-height:22px;padding:4px 7px}#running .panel-group .panel .panel-heading a:focus,#running .panel-group .panel .panel-heading a:hover{text-decoration:none}#running .panel-group .panel .panel-body{padding:0}#running .panel-group .panel .panel-body .list_container{margin-top:0;margin-bottom:0;border:0;border-radius:0}#running .panel-group .panel .panel-body .list_container .list_item{border-bottom:1px solid #ddd}#running .panel-group .panel .panel-body .list_container .list_item:last-child{border-bottom:0}.delete-button,.duplicate-button,.rename-button,.shutdown-button{display:none}.dynamic-instructions{display:inline-block;padding-top:4px}/*!
*
* IPython text editor webapp
*
*/.selected-keymap i.fa{padding:0 5px}.selected-keymap i.fa:before{content:"\f00c"}#mode-menu{overflow:auto;max-height:20em}.edit_app #header{-webkit-box-shadow:0 0 12px 1px rgba(87,87,87,.2);box-shadow:0 0 12px 1px rgba(87,87,87,.2)}.edit_app #menubar .navbar{margin-bottom:-1px}.dirty-indicator{display:inline-block;font:normal normal normal 14px/1 FontAwesome;font-size:inherit;text-rendering:auto;-webkit-font-smoothing:antialiased;-moz-osx-font-smoothing:grayscale;width:20px}.dirty-indicator.pull-left{margin-right:.3em}.dirty-indicator.pull-right{margin-left:.3em}.dirty-indicator-dirty{display:inline-block;font:normal normal normal 14px/1 FontAwesome;font-size:inherit;text-rendering:auto;-webkit-font-smoothing:antialiased;-moz-osx-font-smoothing:grayscale;width:20px}.dirty-indicator-dirty.pull-left{margin-right:.3em}.dirty-indicator-dirty.pull-right{margin-left:.3em}.dirty-indicator-clean{display:inline-block;font:normal normal normal 14px/1 FontAwesome;font-size:inherit;text-rendering:auto;-webkit-font-smoothing:antialiased;-moz-osx-font-smoothing:grayscale;width:20px}.dirty-indicator-clean.pull-left{margin-right:.3em}.dirty-indicator-clean.pull-right{margin-left:.3em}.dirty-indicator-clean:before{display:inline-block;font:normal normal normal 14px/1 FontAwesome;font-size:inherit;text-rendering:auto;-webkit-font-smoothing:antialiased;-moz-osx-font-smoothing:grayscale;content:"\f00c"}.dirty-indicator-clean:before.pull-left{margin-right:.3em}.dirty-indicator-clean:before.pull-right{margin-left:.3em}#filename{font-size:16pt;display:table;padding:0 5px}#current-mode{padding-left:5px;padding-right:5px}#texteditor-backdrop{padding-top:20px;padding-bottom:20px}@media not print{#texteditor-backdrop{background-color:#eee}}@media print{#texteditor-backdrop #texteditor-container .CodeMirror-gutter,#texteditor-backdrop #texteditor-container .CodeMirror-gutters{background-color:#fff}}@media not print{#texteditor-backdrop #texteditor-container .CodeMirror-gutter,#texteditor-backdrop #texteditor-container .CodeMirror-gutters{background-color:#fff}#texteditor-backdrop #texteditor-container{padding:0;background-color:#fff;-webkit-box-shadow:0 0 12px 1px rgba(87,87,87,.2);box-shadow:0 0 12px 1px rgba(87,87,87,.2)}}/*!
*
* IPython notebook
*
*/.ansibold{font-weight:700}.ansiblack{color:#000}.ansired{color:#8b0000}.ansigreen{color:#006400}.ansiyellow{color:#c4a000}.ansiblue{color:#00008b}.ansipurple{color:#9400d3}.ansicyan{color:#4682b4}.ansigray{color:gray}.ansibgblack{background-color:#000}.ansibgred{background-color:red}.ansibggreen{background-color:green}.ansibgyellow{background-color:#ff0}.ansibgblue{background-color:#00f}.ansibgpurple{background-color:#ff00ff}.ansibgcyan{background-color:#0ff}.ansibggray{background-color:gray}div.cell{border:1px solid transparent;display:-webkit-box;-webkit-box-orient:vertical;display:-moz-box;-moz-box-orient:vertical;display:box;box-orient:vertical;box-align:stretch;display:flex;flex-direction:column;align-items:stretch;border-radius:2px;box-sizing:border-box;-moz-box-sizing:border-box;border-width:thin;border-style:solid;width:100%;padding:5px;margin:0;outline:0}div.cell.selected{border-color:#ababab}@media print{div.cell.selected{border-color:transparent}}.edit_mode div.cell.selected{border-color:green}.prompt{min-width:14ex;padding:.4em;margin:0;font-family:monospace;text-align:right;line-height:1.21429em}div.inner_cell{display:-webkit-box;-webkit-box-orient:vertical;display:-moz-box;-moz-box-orient:vertical;display:box;box-orient:vertical;box-align:stretch;display:flex;flex-direction:column;align-items:stretch;-webkit-box-flex:1;-moz-box-flex:1;box-flex:1;flex:1}@-moz-document url-prefix(){div.inner_cell{overflow-x:hidden}}div.input_area{border:1px solid #cfcfcf;border-radius:2px;background:#f7f7f7;line-height:1.21429em}div.prompt:empty{padding-top:0;padding-bottom:0}div.unrecognized_cell{padding:5px 5px 5px 0;display:-webkit-box;-webkit-box-orient:horizontal;display:-moz-box;-moz-box-orient:horizontal;display:box;box-orient:horizontal;box-align:stretch;display:flex;flex-direction:row;align-items:stretch}div.unrecognized_cell .inner_cell{border-radius:2px;padding:5px;font-weight:700;color:red;border:1px solid #cfcfcf;background:#eaeaea}div.unrecognized_cell .inner_cell a,div.unrecognized_cell .inner_cell a:hover{color:inherit;text-decoration:none}@media (max-width:540px){.prompt{text-align:left}div.unrecognized_cell>div.prompt{display:none}}div.code_cell{}div.input{page-break-inside:avoid;display:-webkit-box;-webkit-box-orient:horizontal;display:-moz-box;-moz-box-orient:horizontal;display:box;box-orient:horizontal;box-align:stretch;display:flex;flex-direction:row;align-items:stretch}@media (max-width:540px){div.input{-webkit-box-orient:vertical;-moz-box-orient:vertical;box-orient:vertical;box-align:stretch;display:flex;flex-direction:column;align-items:stretch}}div.input_prompt{color:navy;border-top:1px solid transparent}div.input_area>div.highlight{margin:.4em;border:none;padding:0;background-color:transparent}div.input_area>div.highlight>pre{margin:0;border:none;padding:0;background-color:transparent}.CodeMirror{line-height:1.21429em;font-size:14px;height:auto;background:0 0}.CodeMirror-scroll{overflow-y:hidden;overflow-x:auto}.CodeMirror-lines{padding:.4em}.CodeMirror-linenumber{padding:0 8px 0 4px}.CodeMirror-gutters{border-bottom-left-radius:2px;border-top-left-radius:2px}.CodeMirror pre{padding:0;border:0;border-radius:0}.highlight-base,.highlight-variable{color:#000}.highlight-variable-2{color:#1a1a1a}.highlight-variable-3{color:#333}.highlight-string{color:#BA2121}.highlight-comment{color:#408080;font-style:italic}.highlight-number{color:#080}.highlight-atom{color:#88F}.highlight-keyword{color:green;font-weight:700}.highlight-builtin{color:green}.highlight-error{color:red}.highlight-operator{color:#A2F;font-weight:700}.highlight-meta{color:#A2F}.highlight-def{color:#00f}.highlight-string-2{color:#f50}.highlight-qualifier{color:#555}.highlight-bracket{color:#997}.highlight-tag{color:#170}.highlight-attribute{color:#00c}.highlight-header{color:#00f}.highlight-quote{color:#090}.highlight-link{color:#00c}.cm-s-ipython span.cm-keyword{color:green;font-weight:700}.cm-s-ipython span.cm-atom{color:#88F}.cm-s-ipython span.cm-number{color:#080}.cm-s-ipython span.cm-def{color:#00f}.cm-s-ipython span.cm-variable{color:#000}.cm-s-ipython span.cm-operator{color:#A2F;font-weight:700}.cm-s-ipython span.cm-variable-2{color:#1a1a1a}.cm-s-ipython span.cm-variable-3{color:#333}.cm-s-ipython span.cm-comment{color:#408080;font-style:italic}.cm-s-ipython span.cm-string{color:#BA2121}.cm-s-ipython span.cm-string-2{color:#f50}.cm-s-ipython span.cm-meta{color:#A2F}.cm-s-ipython span.cm-qualifier{color:#555}.cm-s-ipython span.cm-builtin{color:green}.cm-s-ipython span.cm-bracket{color:#997}.cm-s-ipython span.cm-tag{color:#170}.cm-s-ipython span.cm-attribute{color:#00c}.cm-s-ipython span.cm-header{color:#00f}.cm-s-ipython span.cm-quote{color:#090}.cm-s-ipython span.cm-link{color:#00c}.cm-s-ipython span.cm-error{color:red}.cm-s-ipython span.cm-tab{background:url('data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAADAAAAAMCAYAAAAkuj5RAAAAAXNSR0IArs4c6QAAAGFJREFUSMft1LsRQFAQheHPowAKoACx3IgEKtaEHujDjORSgWTH/ZOdnZOcM/sgk/kFFWY0qV8foQwS4MKBCS3qR6ixBJvElOobYAtivseIE120FaowJPN75GMu8j/LfMwNjh4HUpwg4LUAAAAASUVORK5CYII=')right no-repeat}div.output_wrapper{display:-webkit-box;-webkit-box-align:stretch;display:-moz-box;-moz-box-align:stretch;display:box;box-orient:vertical;box-align:stretch;display:flex;flex-direction:column;align-items:stretch;z-index:1}div.output_scroll{height:24em;width:100%;overflow:auto;border-radius:2px;-webkit-box-shadow:inset 0 2px 8px rgba(0,0,0,.8);box-shadow:inset 0 2px 8px rgba(0,0,0,.8);display:block}div.output_collapsed{margin:0;padding:0;display:-webkit-box;-webkit-box-orient:vertical;display:-moz-box;-moz-box-orient:vertical;display:box;box-orient:vertical;box-align:stretch;display:flex;flex-direction:column;align-items:stretch}div.out_prompt_overlay{height:100%;padding:0 .4em;position:absolute;border-radius:2px}div.out_prompt_overlay:hover{-webkit-box-shadow:inset 0 0 1px #000;box-shadow:inset 0 0 1px #000;background:rgba(240,240,240,.5)}div.output_prompt{color:#8b0000}div.output_area{padding:0;page-break-inside:avoid;display:-webkit-box;-webkit-box-orient:horizontal;display:-moz-box;-moz-box-orient:horizontal;display:box;box-orient:horizontal;box-align:stretch;display:flex;flex-direction:row;align-items:stretch}div.output_area .MathJax_Display{text-align:left!important}div.output_area .rendered_html img,div.output_area .rendered_html table{margin-left:0;margin-right:0}div.output_area img,div.output_area svg{max-width:100%;height:auto}div.output_area img.unconfined,div.output_area svg.unconfined{max-width:none}.output{display:-webkit-box;-webkit-box-orient:vertical;display:-moz-box;-moz-box-orient:vertical;display:box;box-orient:vertical;box-align:stretch;display:flex;flex-direction:column;align-items:stretch}@media (max-width:540px){div.output_area{-webkit-box-orient:vertical;-moz-box-orient:vertical;box-orient:vertical;box-align:stretch;display:flex;flex-direction:column;align-items:stretch}}div.output_area pre{margin:0;padding:0;border:0;vertical-align:baseline;color:#000;background-color:transparent;border-radius:0}div.output_subarea{overflow-x:auto;padding:.4em;-webkit-box-flex:1;-moz-box-flex:1;box-flex:1;flex:1;max-width:calc(100% - 14ex)}div.output_text{text-align:left;color:#000;line-height:1.21429em}div.output_stderr{background:#fdd}div.output_latex{text-align:left}div.output_javascript:empty{padding:0}.js-error{color:#8b0000}div.raw_input_container{font-family:monospace;padding-top:5px}span.raw_input_prompt{}input.raw_input{font-family:inherit;font-size:inherit;color:inherit;width:auto;vertical-align:baseline;padding:0 .25em;margin:0 .25em}input.raw_input:focus{box-shadow:none}p.p-space{margin-bottom:10px}div.output_unrecognized{padding:5px;font-weight:700;color:red}div.output_unrecognized a,div.output_unrecognized a:hover{color:inherit;text-decoration:none}.rendered_html{color:#000}.rendered_html em{font-style:italic}.rendered_html strong{font-weight:700}.rendered_html :link,.rendered_html :visited,.rendered_html u{text-decoration:underline}.rendered_html h1{font-size:185.7%;margin:1.08em 0 0;font-weight:700;line-height:1}.rendered_html h2{font-size:157.1%;margin:1.27em 0 0;font-weight:700;line-height:1}.rendered_html h3{font-size:128.6%;margin:1.55em 0 0;font-weight:700;line-height:1}.rendered_html h4{font-size:100%;margin:2em 0 0;font-weight:700;line-height:1}.rendered_html h5,.rendered_html h6{font-size:100%;margin:2em 0 0;font-weight:700;line-height:1;font-style:italic}.rendered_html h1:first-child{margin-top:.538em}.rendered_html h2:first-child{margin-top:.636em}.rendered_html h3:first-child{margin-top:.777em}.rendered_html h4:first-child,.rendered_html h5:first-child,.rendered_html h6:first-child{margin-top:1em}.rendered_html ul{list-style:disc;margin:0 2em;padding-left:0}.rendered_html ul ul{list-style:square;margin:0 2em}.rendered_html ul ul ul{list-style:circle;margin:0 2em}.rendered_html ol{list-style:decimal;margin:0 2em;padding-left:0}.rendered_html ol ol{list-style:upper-alpha;margin:0 2em}.rendered_html ol ol ol{list-style:lower-alpha;margin:0 2em}.rendered_html ol ol ol ol{list-style:lower-roman;margin:0 2em}.rendered_html ol ol ol ol ol{list-style:decimal;margin:0 2em}.rendered_html *+ol,.rendered_html *+ul{margin-top:1em}.rendered_html hr{color:#000;background-color:#000}.rendered_html pre{margin:1em 2em}.rendered_html code,.rendered_html pre{border:0;background-color:#fff;color:#000;font-size:100%;padding:0}.rendered_html blockquote{margin:1em 2em}.rendered_html table{margin-left:auto;margin-right:auto;border:1px solid #000;border-collapse:collapse}.rendered_html td,.rendered_html th,.rendered_html tr{border:1px solid #000;border-collapse:collapse;margin:1em 2em}.rendered_html td,.rendered_html th{text-align:left;vertical-align:middle;padding:4px}.rendered_html th{font-weight:700}.rendered_html *+table{margin-top:1em}.rendered_html p{text-align:left}.rendered_html *+p{margin-top:1em}.rendered_html img{display:block;margin-left:auto;margin-right:auto}.rendered_html *+img{margin-top:1em}.rendered_html img,.rendered_html svg{max-width:100%;height:auto}.rendered_html img.unconfined,.rendered_html svg.unconfined{max-width:none}div.text_cell{display:-webkit-box;-webkit-box-orient:horizontal;display:-moz-box;-moz-box-orient:horizontal;display:box;box-orient:horizontal;box-align:stretch;display:flex;flex-direction:row;align-items:stretch}@media (max-width:540px){div.text_cell>div.prompt{display:none}}div.text_cell_render{outline:0;resize:none;width:inherit;border-style:none;padding:.5em .5em .5em .4em;color:#000;box-sizing:border-box;-moz-box-sizing:border-box;-webkit-box-sizing:border-box}a.anchor-link:link{text-decoration:none;padding:0 20px;visibility:hidden}h1:hover .anchor-link,h2:hover .anchor-link,h3:hover .anchor-link,h4:hover .anchor-link,h5:hover .anchor-link,h6:hover .anchor-link{visibility:visible}.text_cell.rendered .input_area{display:none}.text_cell.rendered .rendered_html{overflow-x:auto}.text_cell.unrendered .text_cell_render{display:none}.cm-header-1,.cm-header-2,.cm-header-3,.cm-header-4,.cm-header-5,.cm-header-6{font-weight:700;font-family:"Helvetica Neue",Helvetica,Arial,sans-serif}.cm-header-1{font-size:185.7%}.cm-header-2{font-size:157.1%}.cm-header-3{font-size:128.6%}.cm-header-4{font-size:110%}.cm-header-5,.cm-header-6{font-size:100%;font-style:italic}/*!
*
* IPython notebook webapp
*
*/@media (max-width:767px){.notebook_app{padding-left:0;padding-right:0}}#ipython-main-app{box-sizing:border-box;-moz-box-sizing:border-box;-webkit-box-sizing:border-box;height:100%}div#notebook_panel{margin:0;padding:0;box-sizing:border-box;-moz-box-sizing:border-box;-webkit-box-sizing:border-box;height:100%}#notebook{font-size:14px;line-height:20px;overflow-y:hidden;overflow-x:auto;width:100%;padding-top:20px;margin:0;outline:0;box-sizing:border-box;-moz-box-sizing:border-box;-webkit-box-sizing:border-box;min-height:100%}@media not print{#notebook-container{padding:15px;background-color:#fff;min-height:0;-webkit-box-shadow:0 0 12px 1px rgba(87,87,87,.2);box-shadow:0 0 12px 1px rgba(87,87,87,.2)}}div.ui-widget-content{border:1px solid #ababab;outline:0}pre.dialog{background-color:#f7f7f7;border:1px solid #ddd;border-radius:2px;padding:.4em .4em .4em 2em}p.dialog{padding:.2em}code,kbd,pre,samp{white-space:pre-wrap}#fonttest{font-family:monospace}p{margin-bottom:0}.end_space{min-height:100px;transition:height .2s ease}.notebook_app #header{-webkit-box-shadow:0 0 12px 1px rgba(87,87,87,.2);box-shadow:0 0 12px 1px rgba(87,87,87,.2)}@media not print{.notebook_app{background-color:#eee}}.celltoolbar{border:thin solid #CFCFCF;border-bottom:none;background:#EEE;border-radius:2px 2px 0 0;width:100%;height:29px;padding-right:4px;-webkit-box-orient:horizontal;-moz-box-orient:horizontal;box-orient:horizontal;box-align:stretch;display:flex;flex-direction:row;align-items:stretch;-webkit-box-pack:end;-moz-box-pack:end;box-pack:end;justify-content:flex-end;font-size:87%;padding-top:3px}@media print{.edit_mode div.cell.selected{border-color:transparent}div.code_cell{page-break-inside:avoid}#notebook-container{width:100%}.celltoolbar{display:none}}.ctb_hideshow{display:none;vertical-align:bottom}.ctb_global_show .ctb_show.ctb_hideshow{display:block}.ctb_global_show .ctb_show+.input_area,.ctb_global_show .ctb_show+div.text_cell_input,.ctb_global_show .ctb_show~div.text_cell_render{border-top-right-radius:0;border-top-left-radius:0}.ctb_global_show .ctb_show~div.text_cell_render{border:1px solid #cfcfcf}.celltoolbar select{color:#555;background-color:#fff;background-image:none;border:1px solid #ccc;-webkit-box-shadow:inset 0 1px 1px rgba(0,0,0,.075);box-shadow:inset 0 1px 1px rgba(0,0,0,.075);-webkit-transition:border-color ease-in-out .15s,box-shadow ease-in-out .15s;-o-transition:border-color ease-in-out .15s,box-shadow ease-in-out .15s;transition:border-color ease-in-out .15s,box-shadow ease-in-out .15s;line-height:1.5;border-radius:1px;width:inherit;font-size:inherit;height:22px;padding:0;display:inline-block}.celltoolbar select:focus{border-color:#66afe9;outline:0;-webkit-box-shadow:inset 0 1px 1px rgba(0,0,0,.075),0 0 8px rgba(102,175,233,.6);box-shadow:inset 0 1px 1px rgba(0,0,0,.075),0 0 8px rgba(102,175,233,.6)}.celltoolbar select::-moz-placeholder{color:#999;opacity:1}.celltoolbar select:-ms-input-placeholder{color:#999}.celltoolbar select::-webkit-input-placeholder{color:#999}.celltoolbar select[disabled],.celltoolbar select[readonly],fieldset[disabled] .celltoolbar select{background-color:#eee;opacity:1}.celltoolbar select[disabled],fieldset[disabled] .celltoolbar select{cursor:not-allowed}textarea.celltoolbar select{height:auto}select.celltoolbar select{height:30px;line-height:30px}select[multiple].celltoolbar select,textarea.celltoolbar select{height:auto}.celltoolbar label{margin-left:5px;margin-right:5px}.completions{position:absolute;z-index:10;overflow:hidden;border:1px solid #ababab;border-radius:2px;-webkit-box-shadow:0 6px 10px -1px #adadad;box-shadow:0 6px 10px -1px #adadad;line-height:1}.completions select{background:#fff;outline:0;border:none;padding:0;margin:0;overflow:auto;font-family:monospace;font-size:110%;color:#000;width:auto}.completions select option.context{color:#286090}#kernel_logo_widget{float:right!important;float:right}#kernel_logo_widget .current_kernel_logo{display:none;margin-top:-1px;margin-bottom:-1px;width:32px;height:32px}#menubar{box-sizing:border-box;-moz-box-sizing:border-box;-webkit-box-sizing:border-box;margin-top:1px}#menubar .navbar{border-top:1px;border-radius:0 0 2px 2px;margin-bottom:0}#menubar .navbar-toggle{float:left;padding-top:7px;padding-bottom:7px;border:none}#menubar .navbar-collapse{clear:left}.nav-wrapper{border-bottom:1px solid #e7e7e7}i.menu-icon{padding-top:4px}ul#help_menu li a{overflow:hidden;padding-right:2.2em}ul#help_menu li a i{margin-right:-1.2em}.dropdown-submenu{position:relative}.dropdown-submenu>.dropdown-menu{top:0;left:100%;margin-top:-6px;margin-left:-1px}.dropdown-submenu:hover>.dropdown-menu{display:block}.dropdown-submenu>a:after{font:normal normal normal 14px/1 FontAwesome;font-size:inherit;text-rendering:auto;-webkit-font-smoothing:antialiased;-moz-osx-font-smoothing:grayscale;display:block;content:"\f0da";float:right;color:#333;margin-top:2px;margin-right:-10px}.dropdown-submenu>a:after.pull-left{margin-right:.3em}.dropdown-submenu>a:after.pull-right{margin-left:.3em}.dropdown-submenu:hover>a:after{color:#262626}.dropdown-submenu.pull-left{float:none}.dropdown-submenu.pull-left>.dropdown-menu{left:-100%;margin-left:10px}#notification_area{float:right!important;float:right;z-index:10}.indicator_area{float:right!important;float:right;color:#777;margin-left:5px;margin-right:5px;z-index:10;text-align:center;width:auto}#kernel_indicator{float:right!important;float:right;color:#777;margin-left:5px;margin-right:5px;z-index:10;text-align:center;width:auto;border-left:1px solid}#kernel_indicator .kernel_indicator_name{padding-left:5px;padding-right:5px}#modal_indicator{float:right!important;float:right;color:#777;margin-left:5px;margin-right:5px;z-index:10;text-align:center;width:auto}#readonly-indicator{float:right!important;float:right;color:#777;z-index:10;text-align:center;width:auto;display:none;margin:2px 0 0}.modal_indicator:before{width:1.28571429em;text-align:center}.edit_mode .modal_indicator:before{display:inline-block;font:normal normal normal 14px/1 FontAwesome;font-size:inherit;text-rendering:auto;-webkit-font-smoothing:antialiased;-moz-osx-font-smoothing:grayscale;content:"\f040"}.edit_mode .modal_indicator:before.pull-left{margin-right:.3em}.edit_mode .modal_indicator:before.pull-right{margin-left:.3em}.command_mode .modal_indicator:before{display:inline-block;font:normal normal normal 14px/1 FontAwesome;font-size:inherit;text-rendering:auto;-webkit-font-smoothing:antialiased;-moz-osx-font-smoothing:grayscale;content:' '}.command_mode .modal_indicator:before.pull-left{margin-right:.3em}.command_mode .modal_indicator:before.pull-right{margin-left:.3em}.kernel_idle_icon:before{display:inline-block;font:normal normal normal 14px/1 FontAwesome;font-size:inherit;text-rendering:auto;-webkit-font-smoothing:antialiased;-moz-osx-font-smoothing:grayscale;content:"\f10c"}.kernel_idle_icon:before.pull-left{margin-right:.3em}.kernel_idle_icon:before.pull-right{margin-left:.3em}.kernel_busy_icon:before{display:inline-block;font:normal normal normal 14px/1 FontAwesome;font-size:inherit;text-rendering:auto;-webkit-font-smoothing:antialiased;-moz-osx-font-smoothing:grayscale;content:"\f111"}.kernel_busy_icon:before.pull-left{margin-right:.3em}.kernel_busy_icon:before.pull-right{margin-left:.3em}.kernel_dead_icon:before{display:inline-block;font:normal normal normal 14px/1 FontAwesome;font-size:inherit;text-rendering:auto;-webkit-font-smoothing:antialiased;-moz-osx-font-smoothing:grayscale;content:"\f1e2"}.kernel_dead_icon:before.pull-left{margin-right:.3em}.kernel_dead_icon:before.pull-right{margin-left:.3em}.kernel_disconnected_icon:before{display:inline-block;font:normal normal normal 14px/1 FontAwesome;font-size:inherit;text-rendering:auto;-webkit-font-smoothing:antialiased;-moz-osx-font-smoothing:grayscale;content:"\f127"}.kernel_disconnected_icon:before.pull-left{margin-right:.3em}.kernel_disconnected_icon:before.pull-right{margin-left:.3em}.notification_widget{z-index:10;background:rgba(240,240,240,.5);margin-right:4px;color:#333;background-color:#fff;border-color:#ccc}.notification_widget.active,.notification_widget.focus,.notification_widget:active,.notification_widget:focus,.notification_widget:hover,.open>.dropdown-toggle.notification_widget{color:#333;background-color:#e6e6e6;border-color:#adadad}.notification_widget.active,.notification_widget:active,.open>.dropdown-toggle.notification_widget{background-image:none}.notification_widget.disabled,.notification_widget.disabled.active,.notification_widget.disabled.focus,.notification_widget.disabled:active,.notification_widget.disabled:focus,.notification_widget.disabled:hover,.notification_widget[disabled],.notification_widget[disabled].active,.notification_widget[disabled].focus,.notification_widget[disabled]:active,.notification_widget[disabled]:focus,.notification_widget[disabled]:hover,fieldset[disabled] .notification_widget,fieldset[disabled] .notification_widget.active,fieldset[disabled] .notification_widget.focus,fieldset[disabled] .notification_widget:active,fieldset[disabled] .notification_widget:focus,fieldset[disabled] .notification_widget:hover{background-color:#fff;border-color:#ccc}.notification_widget .badge{color:#fff;background-color:#333}.notification_widget.warning{color:#fff;background-color:#f0ad4e;border-color:#eea236}.notification_widget.warning.active,.notification_widget.warning.focus,.notification_widget.warning:active,.notification_widget.warning:focus,.notification_widget.warning:hover,.open>.dropdown-toggle.notification_widget.warning{color:#fff;background-color:#ec971f;border-color:#d58512}.notification_widget.warning.active,.notification_widget.warning:active,.open>.dropdown-toggle.notification_widget.warning{background-image:none}.notification_widget.warning.disabled,.notification_widget.warning.disabled.active,.notification_widget.warning.disabled.focus,.notification_widget.warning.disabled:active,.notification_widget.warning.disabled:focus,.notification_widget.warning.disabled:hover,.notification_widget.warning[disabled],.notification_widget.warning[disabled].active,.notification_widget.warning[disabled].focus,.notification_widget.warning[disabled]:active,.notification_widget.warning[disabled]:focus,.notification_widget.warning[disabled]:hover,fieldset[disabled] .notification_widget.warning,fieldset[disabled] .notification_widget.warning.active,fieldset[disabled] .notification_widget.warning.focus,fieldset[disabled] .notification_widget.warning:active,fieldset[disabled] .notification_widget.warning:focus,fieldset[disabled] .notification_widget.warning:hover{background-color:#f0ad4e;border-color:#eea236}.notification_widget.warning .badge{color:#f0ad4e;background-color:#fff}.notification_widget.success{color:#fff;background-color:#5cb85c;border-color:#4cae4c}.notification_widget.success.active,.notification_widget.success.focus,.notification_widget.success:active,.notification_widget.success:focus,.notification_widget.success:hover,.open>.dropdown-toggle.notification_widget.success{color:#fff;background-color:#449d44;border-color:#398439}.notification_widget.success.active,.notification_widget.success:active,.open>.dropdown-toggle.notification_widget.success{background-image:none}.notification_widget.success.disabled,.notification_widget.success.disabled.active,.notification_widget.success.disabled.focus,.notification_widget.success.disabled:active,.notification_widget.success.disabled:focus,.notification_widget.success.disabled:hover,.notification_widget.success[disabled],.notification_widget.success[disabled].active,.notification_widget.success[disabled].focus,.notification_widget.success[disabled]:active,.notification_widget.success[disabled]:focus,.notification_widget.success[disabled]:hover,fieldset[disabled] .notification_widget.success,fieldset[disabled] .notification_widget.success.active,fieldset[disabled] .notification_widget.success.focus,fieldset[disabled] .notification_widget.success:active,fieldset[disabled] .notification_widget.success:focus,fieldset[disabled] .notification_widget.success:hover{background-color:#5cb85c;border-color:#4cae4c}.notification_widget.success .badge{color:#5cb85c;background-color:#fff}.notification_widget.info{color:#fff;background-color:#5bc0de;border-color:#46b8da}.notification_widget.info.active,.notification_widget.info.focus,.notification_widget.info:active,.notification_widget.info:focus,.notification_widget.info:hover,.open>.dropdown-toggle.notification_widget.info{color:#fff;background-color:#31b0d5;border-color:#269abc}.notification_widget.info.active,.notification_widget.info:active,.open>.dropdown-toggle.notification_widget.info{background-image:none}.notification_widget.info.disabled,.notification_widget.info.disabled.active,.notification_widget.info.disabled.focus,.notification_widget.info.disabled:active,.notification_widget.info.disabled:focus,.notification_widget.info.disabled:hover,.notification_widget.info[disabled],.notification_widget.info[disabled].active,.notification_widget.info[disabled].focus,.notification_widget.info[disabled]:active,.notification_widget.info[disabled]:focus,.notification_widget.info[disabled]:hover,fieldset[disabled] .notification_widget.info,fieldset[disabled] .notification_widget.info.active,fieldset[disabled] .notification_widget.info.focus,fieldset[disabled] .notification_widget.info:active,fieldset[disabled] .notification_widget.info:focus,fieldset[disabled] .notification_widget.info:hover{background-color:#5bc0de;border-color:#46b8da}.notification_widget.info .badge{color:#5bc0de;background-color:#fff}.notification_widget.danger{color:#fff;background-color:#d9534f;border-color:#d43f3a}.notification_widget.danger.active,.notification_widget.danger.focus,.notification_widget.danger:active,.notification_widget.danger:focus,.notification_widget.danger:hover,.open>.dropdown-toggle.notification_widget.danger{color:#fff;background-color:#c9302c;border-color:#ac2925}.notification_widget.danger.active,.notification_widget.danger:active,.open>.dropdown-toggle.notification_widget.danger{background-image:none}.notification_widget.danger.disabled,.notification_widget.danger.disabled.active,.notification_widget.danger.disabled.focus,.notification_widget.danger.disabled:active,.notification_widget.danger.disabled:focus,.notification_widget.danger.disabled:hover,.notification_widget.danger[disabled],.notification_widget.danger[disabled].active,.notification_widget.danger[disabled].focus,.notification_widget.danger[disabled]:active,.notification_widget.danger[disabled]:focus,.notification_widget.danger[disabled]:hover,fieldset[disabled] .notification_widget.danger,fieldset[disabled] .notification_widget.danger.active,fieldset[disabled] .notification_widget.danger.focus,fieldset[disabled] .notification_widget.danger:active,fieldset[disabled] .notification_widget.danger:focus,fieldset[disabled] .notification_widget.danger:hover{background-color:#d9534f;border-color:#d43f3a}.notification_widget.danger .badge{color:#d9534f;background-color:#fff}div#pager{background-color:#fff;font-size:14px;line-height:20px;overflow:hidden;display:none;position:fixed;bottom:0;width:100%;max-height:50%;padding-top:8px;-webkit-box-shadow:0 0 12px 1px rgba(87,87,87,.2);box-shadow:0 0 12px 1px rgba(87,87,87,.2);z-index:100;top:auto!important}div#pager pre{line-height:1.21429em;color:#000;background-color:#f7f7f7;padding:.4em}div#pager #pager-button-area{position:absolute;top:8px;right:20px}div#pager #pager-contents{position:relative;overflow:auto;width:100%;height:100%}div#pager #pager-contents #pager-container{position:relative;padding:15px 0;box-sizing:border-box;-moz-box-sizing:border-box;-webkit-box-sizing:border-box}div#pager .ui-resizable-handle{top:0;height:8px;background:#f7f7f7;border-top:1px solid #cfcfcf;border-bottom:1px solid #cfcfcf}div#pager .ui-resizable-handle::after{content:'';top:2px;left:50%;height:3px;width:30px;margin-left:-15px;position:absolute;border-top:1px solid #cfcfcf}.quickhelp{display:-webkit-box;-webkit-box-orient:horizontal;display:-moz-box;-moz-box-orient:horizontal;display:box;box-orient:horizontal;box-align:stretch;display:flex;flex-direction:row;align-items:stretch}.shortcut_key{display:inline-block;width:20ex;text-align:right;font-family:monospace}.shortcut_descr{display:inline-block;-webkit-box-flex:1;-moz-box-flex:1;box-flex:1;flex:1}span.save_widget{margin-top:6px}span.save_widget span.filename{height:1em;line-height:1em;padding:3px;margin-left:16px;border:none;font-size:146.5%;border-radius:2px}span.save_widget span.filename:hover{background-color:#e6e6e6}span.autosave_status,span.checkpoint_status{font-size:small}@media (max-width:767px){span.save_widget{font-size:small}span.autosave_status,span.checkpoint_status{display:none}}@media (min-width:768px)and (max-width:991px){span.checkpoint_status{display:none}span.autosave_status{font-size:x-small}}.toolbar{padding:0;margin-left:-5px;margin-top:2px;margin-bottom:5px;box-sizing:border-box;-moz-box-sizing:border-box;-webkit-box-sizing:border-box}.toolbar label,.toolbar select{width:auto;vertical-align:middle;margin-bottom:0;display:inline;font-size:92%;margin-left:.3em;margin-right:.3em;padding:3px 0 0}.toolbar .btn{padding:2px 8px}.toolbar .btn-group{margin-top:0;margin-left:5px}#maintoolbar{margin-bottom:-3px;margin-top:-8px;border:0;min-height:27px;margin-left:0;padding-top:11px;padding-bottom:3px}#maintoolbar .navbar-text{float:none;vertical-align:middle;text-align:right;margin-left:5px;margin-right:0;margin-top:0}.select-xs{height:24px}@-moz-keyframes fadeOut{from{opacity:1}to{opacity:0}}@-webkit-keyframes fadeOut{from{opacity:1}to{opacity:0}}@-moz-keyframes fadeIn{from{opacity:0}to{opacity:1}}@-webkit-keyframes fadeIn{from{opacity:0}to{opacity:1}}.bigtooltip{overflow:auto;height:200px;-webkit-transition-property:height;-webkit-transition-duration:500ms;-moz-transition-property:height;-moz-transition-duration:500ms;transition-property:height;transition-duration:500ms}.smalltooltip{-webkit-transition-property:height;-webkit-transition-duration:500ms;-moz-transition-property:height;-moz-transition-duration:500ms;transition-property:height;transition-duration:500ms;text-overflow:ellipsis;overflow:hidden;height:80px}.tooltipbuttons{position:absolute;padding-right:15px;top:0;right:0}.tooltiptext{padding-right:30px}.ipython_tooltip{max-width:700px;animation:fadeOut 400ms;-webkit-animation:fadeIn 400ms;-moz-animation:fadeIn 400ms;animation:fadeIn 400ms;vertical-align:middle;background-color:#f7f7f7;overflow:visible;border:1px solid #ababab;outline:0;padding:3px 3px 3px 7px;padding-left:7px;font-family:monospace;min-height:50px;-moz-box-shadow:0 6px 10px -1px #adadad;-webkit-box-shadow:0 6px 10px -1px #adadad;box-shadow:0 6px 10px -1px #adadad;border-radius:2px;position:absolute;z-index:1000}.ipython_tooltip a{float:right}.ipython_tooltip .tooltiptext pre{border:0;border-radius:0;font-size:100%;background-color:#f7f7f7}.pretooltiparrow{left:0;margin:0;top:-16px;width:40px;height:16px;overflow:hidden;position:absolute}.pretooltiparrow:before{background-color:#f7f7f7;border:1px solid #ababab;z-index:11;content:"";position:absolute;left:15px;top:10px;width:25px;height:25px;-webkit-transform:rotate(45deg);-moz-transform:rotate(45deg);-ms-transform:rotate(45deg);-o-transform:rotate(45deg)}.terminal-app{background:#eee}.terminal-app #header{background:#fff;-webkit-box-shadow:0 0 12px 1px rgba(87,87,87,.2);box-shadow:0 0 12px 1px rgba(87,87,87,.2)}.terminal-app .terminal{float:left;font-family:monospace;color:#fff;background:#000;padding:.4em;border-radius:2px;-webkit-box-shadow:0 0 12px 1px rgba(87,87,87,.4);box-shadow:0 0 12px 1px rgba(87,87,87,.4)}.terminal-app .terminal,.terminal-app .terminal dummy-screen{line-height:1em;font-size:14px}.terminal-app .terminal-cursor{color:#000;background:#fff}.terminal-app #terminado-container{margin-top:20px}
/*# sourceMappingURL=style.min.css.map */
    </style>
<style type="text/css">
    .highlight .hll { background-color: #ffffcc }
.highlight  { background: #f8f8f8; }
.highlight .c { color: #408080; font-style: italic } /* Comment */
.highlight .err { border: 1px solid #FF0000 } /* Error */
.highlight .k { color: #008000; font-weight: bold } /* Keyword */
.highlight .o { color: #666666 } /* Operator */
.highlight .cm { color: #408080; font-style: italic } /* Comment.Multiline */
.highlight .cp { color: #BC7A00 } /* Comment.Preproc */
.highlight .c1 { color: #408080; font-style: italic } /* Comment.Single */
.highlight .cs { color: #408080; font-style: italic } /* Comment.Special */
.highlight .gd { color: #A00000 } /* Generic.Deleted */
.highlight .ge { font-style: italic } /* Generic.Emph */
.highlight .gr { color: #FF0000 } /* Generic.Error */
.highlight .gh { color: #000080; font-weight: bold } /* Generic.Heading */
.highlight .gi { color: #00A000 } /* Generic.Inserted */
.highlight .go { color: #888888 } /* Generic.Output */
.highlight .gp { color: #000080; font-weight: bold } /* Generic.Prompt */
.highlight .gs { font-weight: bold } /* Generic.Strong */
.highlight .gu { color: #800080; font-weight: bold } /* Generic.Subheading */
.highlight .gt { color: #0044DD } /* Generic.Traceback */
.highlight .kc { color: #008000; font-weight: bold } /* Keyword.Constant */
.highlight .kd { color: #008000; font-weight: bold } /* Keyword.Declaration */
.highlight .kn { color: #008000; font-weight: bold } /* Keyword.Namespace */
.highlight .kp { color: #008000 } /* Keyword.Pseudo */
.highlight .kr { color: #008000; font-weight: bold } /* Keyword.Reserved */
.highlight .kt { color: #B00040 } /* Keyword.Type */
.highlight .m { color: #666666 } /* Literal.Number */
.highlight .s { color: #BA2121 } /* Literal.String */
.highlight .na { color: #7D9029 } /* Name.Attribute */
.highlight .nb { color: #008000 } /* Name.Builtin */
.highlight .nc { color: #0000FF; font-weight: bold } /* Name.Class */
.highlight .no { color: #880000 } /* Name.Constant */
.highlight .nd { color: #AA22FF } /* Name.Decorator */
.highlight .ni { color: #999999; font-weight: bold } /* Name.Entity */
.highlight .ne { color: #D2413A; font-weight: bold } /* Name.Exception */
.highlight .nf { color: #0000FF } /* Name.Function */
.highlight .nl { color: #A0A000 } /* Name.Label */
.highlight .nn { color: #0000FF; font-weight: bold } /* Name.Namespace */
.highlight .nt { color: #008000; font-weight: bold } /* Name.Tag */
.highlight .nv { color: #19177C } /* Name.Variable */
.highlight .ow { color: #AA22FF; font-weight: bold } /* Operator.Word */
.highlight .w { color: #bbbbbb } /* Text.Whitespace */
.highlight .mb { color: #666666 } /* Literal.Number.Bin */
.highlight .mf { color: #666666 } /* Literal.Number.Float */
.highlight .mh { color: #666666 } /* Literal.Number.Hex */
.highlight .mi { color: #666666 } /* Literal.Number.Integer */
.highlight .mo { color: #666666 } /* Literal.Number.Oct */
.highlight .sb { color: #BA2121 } /* Literal.String.Backtick */
.highlight .sc { color: #BA2121 } /* Literal.String.Char */
.highlight .sd { color: #BA2121; font-style: italic } /* Literal.String.Doc */
.highlight .s2 { color: #BA2121 } /* Literal.String.Double */
.highlight .se { color: #BB6622; font-weight: bold } /* Literal.String.Escape */
.highlight .sh { color: #BA2121 } /* Literal.String.Heredoc */
.highlight .si { color: #BB6688; font-weight: bold } /* Literal.String.Interpol */
.highlight .sx { color: #008000 } /* Literal.String.Other */
.highlight .sr { color: #BB6688 } /* Literal.String.Regex */
.highlight .s1 { color: #BA2121 } /* Literal.String.Single */
.highlight .ss { color: #19177C } /* Literal.String.Symbol */
.highlight .bp { color: #008000 } /* Name.Builtin.Pseudo */
.highlight .vc { color: #19177C } /* Name.Variable.Class */
.highlight .vg { color: #19177C } /* Name.Variable.Global */
.highlight .vi { color: #19177C } /* Name.Variable.Instance */
.highlight .il { color: #666666 } /* Literal.Number.Integer.Long */
    </style>


<style type="text/css">
/* Overrides of notebook CSS for static HTML export */
body {
  overflow: visible;
  padding: 8px;
}

div#notebook {
  overflow: visible;
  border-top: none;
}

@media print {
  div.cell {
    display: block;
    page-break-inside: avoid;
  }
  div.output_wrapper {
    display: block;
    page-break-inside: avoid;
  }
  div.output {
    display: block;
    page-break-inside: avoid;
  }
}
</style>

<!-- Custom stylesheet, it must be in the same directory as the html file -->
<link rel="stylesheet" href="custom.css">

<!-- Loading mathjax macro -->
<!-- Load mathjax -->
    <script src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS_HTML"></script>
    <!-- MathJax configuration -->
    <script type="text/x-mathjax-config">
    MathJax.Hub.Config({
        tex2jax: {
            inlineMath: [ ['$','$'], ["\\(","\\)"] ],
            displayMath: [ ['$$','$$'], ["\\[","\\]"] ],
            processEscapes: true,
            processEnvironments: true
        },
        // Center justify equations in code and markdown cells. Elsewhere
        // we use CSS to left justify single line equations in code cells.
        displayAlign: 'center',
        "HTML-CSS": {
            styles: {'.MathJax_Display': {"margin": 0}},
            linebreaks: { automatic: true }
        }
    });
    </script>
    <!-- End of mathjax configuration --></head>
<body>
  <div tabindex="-1" id="notebook" class="border-box-sizing">
    <div class="container" id="notebook-container">

<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h1 id="Analysing-twitter-stream">Analysing twitter stream<a class="anchor-link" href="#Analysing-twitter-stream">&#182;</a></h1><p>For this study the tweetpy streamer will be used.</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[1]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython2"><pre><span class="kn">from</span> <span class="nn">tweepy.streaming</span> <span class="kn">import</span> <span class="n">StreamListener</span>
<span class="kn">from</span> <span class="nn">tweepy</span> <span class="kn">import</span> <span class="n">Stream</span>
<span class="kn">from</span> <span class="nn">tweepy</span> <span class="kn">import</span> <span class="n">OAuthHandler</span>

<span class="kn">from</span> <span class="nn">textblob</span> <span class="kn">import</span> <span class="n">TextBlob</span>

<span class="kn">import</span> <span class="nn">json</span>
<span class="kn">import</span> <span class="nn">pandas</span> <span class="kn">as</span> <span class="nn">pd</span>

<span class="o">%</span><span class="k">matplotlib</span> inline
<span class="kn">import</span> <span class="nn">matplotlib.pyplot</span> <span class="kn">as</span> <span class="nn">plt</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h3 id="Import-keys">Import keys<a class="anchor-link" href="#Import-keys">&#182;</a></h3><p>These are my personal keys, not included in this file.</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[2]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython2"><pre><span class="kn">import</span> <span class="nn">myKeys</span>

<span class="n">api_key</span> <span class="o">=</span> <span class="n">myKeys</span><span class="o">.</span><span class="n">api_key</span>
<span class="n">api_secret</span> <span class="o">=</span> <span class="n">myKeys</span><span class="o">.</span><span class="n">api_secret</span>
<span class="n">access_token_key</span> <span class="o">=</span> <span class="n">myKeys</span><span class="o">.</span><span class="n">access_token_key</span>
<span class="n">access_token_secret</span> <span class="o">=</span> <span class="n">myKeys</span><span class="o">.</span><span class="n">access_token_secret</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h3 id="Create-a-listener-to-handle-everey-tweet">Create a listener to handle everey tweet<a class="anchor-link" href="#Create-a-listener-to-handle-everey-tweet">&#182;</a></h3><p>This class defines a handler for the tweet event. This class is the spine of this exploration's processing. It receives every tweet and loads it from the json format, along with the tweet sentiment into a pandas DataFrame. It adds the score of every tweet to a sentimentIntegral variable that stores the result score of the labels being tracked.</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[3]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython2"><pre><span class="k">class</span> <span class="nc">ColorListener</span><span class="p">(</span><span class="n">StreamListener</span><span class="p">):</span>

    <span class="k">def</span> <span class="nf">__init__</span><span class="p">(</span><span class="bp">self</span><span class="p">):</span>
        <span class="bp">self</span><span class="o">.</span><span class="n">sentimentIntegral</span> <span class="o">=</span> <span class="mi">0</span>
        <span class="bp">self</span><span class="o">.</span><span class="n">tweets</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">DataFrame</span><span class="p">(</span><span class="n">columns</span><span class="o">=</span><span class="p">(</span><span class="s">&#39;tweet&#39;</span><span class="p">,</span> <span class="s">&#39;sentiment&#39;</span><span class="p">))</span>

    <span class="k">def</span> <span class="nf">on_data</span><span class="p">(</span><span class="bp">self</span><span class="p">,</span> <span class="n">data</span><span class="p">):</span>
        <span class="k">try</span><span class="p">:</span>
            <span class="n">tweet</span> <span class="o">=</span> <span class="n">json</span><span class="o">.</span><span class="n">loads</span><span class="p">(</span><span class="n">data</span><span class="p">)</span>
            <span class="n">blob</span> <span class="o">=</span> <span class="n">TextBlob</span><span class="p">(</span><span class="n">tweet</span><span class="p">[</span><span class="s">&#39;text&#39;</span><span class="p">])</span>
            <span class="bp">self</span><span class="o">.</span><span class="n">sentimentIntegral</span> <span class="o">+=</span> <span class="n">blob</span><span class="o">.</span><span class="n">sentiment</span><span class="p">[</span><span class="mi">0</span><span class="p">]</span>
            <span class="k">print</span> <span class="s">&quot;{0:.2f}&quot;</span><span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="nb">round</span><span class="p">(</span><span class="n">blob</span><span class="o">.</span><span class="n">sentiment</span><span class="p">[</span><span class="mi">0</span><span class="p">],</span><span class="mi">2</span><span class="p">)),</span> <span class="s">&quot;{0:.2f}&quot;</span><span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="nb">round</span><span class="p">(</span><span class="bp">self</span><span class="o">.</span><span class="n">sentimentIntegral</span><span class="p">,</span><span class="mi">2</span><span class="p">))</span>
            <span class="n">row</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">Series</span><span class="p">([</span><span class="n">tweet</span><span class="p">[</span><span class="s">&#39;text&#39;</span><span class="p">],</span> <span class="n">blob</span><span class="o">.</span><span class="n">sentiment</span><span class="p">[</span><span class="mi">0</span><span class="p">]],</span> <span class="n">index</span><span class="o">=</span><span class="p">[</span><span class="s">&#39;tweet&#39;</span><span class="p">,</span> <span class="s">&#39;sentiment&#39;</span><span class="p">])</span>
            <span class="bp">self</span><span class="o">.</span><span class="n">tweets</span> <span class="o">=</span> <span class="bp">self</span><span class="o">.</span><span class="n">tweets</span><span class="o">.</span><span class="n">append</span><span class="p">(</span><span class="n">row</span><span class="p">,</span> <span class="n">ignore_index</span><span class="o">=</span><span class="bp">True</span><span class="p">)</span>
        <span class="k">except</span> <span class="ne">UnboundLocalError</span><span class="p">:</span>
            <span class="k">raise</span> <span class="ne">UnboundLocalError</span>
        <span class="k">except</span><span class="p">:</span>
            <span class="k">pass</span>
        <span class="k">return</span> <span class="bp">True</span>

    <span class="k">def</span> <span class="nf">getTotalScore</span><span class="p">(</span><span class="bp">self</span><span class="p">):</span>
        <span class="k">return</span> <span class="bp">self</span><span class="o">.</span><span class="n">sentimentIntegral</span>

    <span class="k">def</span> <span class="nf">on_error</span><span class="p">(</span><span class="bp">self</span><span class="p">,</span> <span class="n">status</span><span class="p">):</span>
        <span class="k">print</span> <span class="s">&quot;Error: &quot;</span><span class="p">,</span> <span class="n">status</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h3 id="Instance-and-running">Instance and running<a class="anchor-link" href="#Instance-and-running">&#182;</a></h3><p>The listener object is created and hooked to the twitter stream with the proper authentication. The stream is later filtered with a specific search term, which is selected to represent a specific social phenomena.</p>
<p><strong>This cell must be stopped from the toolbar</strong> otherwise it will feed from the tweeter stream without stop.</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[&nbsp;]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython2"><pre><span class="n">cListener</span> <span class="o">=</span> <span class="n">ColorListener</span><span class="p">()</span>
<span class="n">auth</span> <span class="o">=</span> <span class="n">OAuthHandler</span><span class="p">(</span><span class="n">api_key</span><span class="p">,</span> <span class="n">api_secret</span><span class="p">)</span>
<span class="n">auth</span><span class="o">.</span><span class="n">set_access_token</span><span class="p">(</span><span class="n">access_token_key</span><span class="p">,</span> <span class="n">access_token_secret</span><span class="p">)</span>

<span class="n">stream</span> <span class="o">=</span> <span class="n">Stream</span><span class="p">(</span><span class="n">auth</span><span class="p">,</span> <span class="n">cListener</span><span class="p">)</span>

<span class="c"># Start reading stream for english tweets with the color words</span>
<span class="n">stream</span><span class="o">.</span><span class="n">filter</span><span class="p">(</span><span class="n">languages</span><span class="o">=</span><span class="p">[</span><span class="s">&#39;en&#39;</span><span class="p">],</span> <span class="n">track</span><span class="o">=</span><span class="p">[</span><span class="s">&#39;red&#39;</span><span class="p">,</span> <span class="s">&#39;green&#39;</span><span class="p">,</span><span class="s">&#39;blue&#39;</span><span class="p">])</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h3 id="Analize-DataFrame">Analize DataFrame<a class="anchor-link" href="#Analize-DataFrame">&#182;</a></h3><p>Now we hawe a pandas dataframe inside the cListener object we can analyze.</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[5]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython2"><pre><span class="n">df</span> <span class="o">=</span> <span class="n">cListener</span><span class="o">.</span><span class="n">tweets</span>
<span class="k">print</span> <span class="nb">len</span><span class="p">(</span><span class="n">df</span><span class="o">.</span><span class="n">index</span><span class="p">)</span> <span class="c"># Number of rows</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt"></div>
<div class="output_subarea output_stream output_stdout output_text">
<pre>1115
</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[6]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython2"><pre><span class="n">df</span><span class="o">.</span><span class="n">head</span><span class="p">()</span> <span class="c"># How the data looks like</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt output_prompt">Out[6]:</div>

<div class="output_html rendered_html output_subarea output_execute_result">
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>tweet</th>
      <th>sentiment</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>RT @5REDVELVET: [OFFICIAL] 160315 RED VELVET #...</td>
      <td>-0.375000</td>
    </tr>
    <tr>
      <th>1</th>
      <td>RT @WampsBraintree: Wamp Train scheduled for 5...</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>2</th>
      <td>RT @thickred3x: Order Red &amp;amp; @JovanJordanXX...</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>3</th>
      <td>@lipdistrikt Thks 4 following! - Please vote f...</td>
      <td>0.166667</td>
    </tr>
    <tr>
      <th>4</th>
      <td>RT @UFCONFOX: Dustin Poirier vs. Bobby Green j...</td>
      <td>-0.200000</td>
    </tr>
  </tbody>
</table>
</div>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[9]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython2"><pre><span class="n">df</span><span class="o">.</span><span class="n">plot</span><span class="p">(</span><span class="n">figsize</span><span class="o">=</span><span class="p">(</span><span class="mi">16</span><span class="p">,</span> <span class="mi">8</span><span class="p">))</span> <span class="c"># Plot the sentiment as a time series</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt output_prompt">Out[9]:</div>


<div class="output_text output_subarea output_execute_result">
<pre>&lt;matplotlib.axes._subplots.AxesSubplot at 0x110f60090&gt;</pre>
</div>

</div>

<div class="output_area"><div class="prompt"></div>


<div class="output_png output_subarea ">
<img src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAA6cAAAHfCAYAAACs8q71AAAABHNCSVQICAgIfAhkiAAAAAlwSFlz
AAALEgAACxIB0t1+/AAAIABJREFUeJzsvXm0ZVV17z9P9QUUBYIiqKAJapr3onk6jE2G4osx6sj7
kUTzcERjotHEGKPR57MhIZYkUTHPaLCLqBFR7LEBpBEiIEKkM4g0AkVPFWBBNbfq9vec8/tjO9nz
zLPavdduztnfzxiMW9x7zt5r772a+V3fudbuDYdDAgAAAAAAAAAAmmRV0wUAAAAAAAAAAAAgTgEA
AAAAAAAANA7EKQAAAAAAAACAxoE4BQAAAAAAAADQOBCnAAAAAAAAAAAaB+IUAAAAAAAAAEDjJBGn
vV7vM71e74Fer3ed4zMn93q9W3u93rW9Xu+pKc4LAAAAAAAAAGA6SOWcfpaIfsf2x16v92Ii+sXh
cPhEIvoLIvq3ROcFAAAAAAAAADAFJBGnw+HwB0S0y/GRY4notJ9/9goi2tzr9Q5LcW4AAAAAAAAA
AJNPXWtOH0NE94j/3/bz3wEAAAAAAAAAALSm6QJoer3esOkyAAAAAAAAAACohuFw2DP9vi5xuo2I
Hif+/7E//52R4RD6FFTD0UcTfec7RE9+svnvW7ZsoS1bttRaJgAY1D9QNf/4j0Szs0Tve9/431D/
6uHv/56o1yN6z3uaLkn7QB0ETYL6Vx+9nlGXElHatN7ez/8zcSYRvernhXkmEe0eDocPJDw3AMFg
7gMA0FWGQ/SBTTMY4BkAAICNJM5pr9f7IhEdQ0SH9Hq9u4no3US0joiGw+HwlOFweE6v13tJr9fb
SkSzRPTqFOcFIBYEZgCALoM+sHnwDAAAwE4ScTocDv8o4DNvTHEuAMrgCwiOOeaYWsoBgAnUP1A1
LmGE+lcPEKd2UAdBk6D+tYO6dusFoBX4ggJ0TKBJUP9AHUCcNgvSeu2gDoImQf1rB63brReAKsGM
NQCgy6APbB48AwDS8fjHP57uuuuuposBLBx11FF05513Rn0H4hR0DgQFAICuAmHUPLj/AKTjrrvu
wls+WoxrV14bSOsFnQKBGQCgy6APbB48AwAAsANxCjoFggIAQJdBH9g8WHMKAAB2IE5Bp0BgBgDo
MugDmwfPAAAA7ECcAgAAAB0Bwqh58AwAAMAOxCnoFAgKAABdBn1g8yCtFwCQkpe85CX0+c9/vuli
JAO79YJOgcAMANBl0Ac2D54BAKAo73nPe+i2226j00477eHfnXPOOY2U5dWvfjU97nGPoxNPPDHp
ceGcgk6BoAAA0HXQBzYLxiEAALADcQo6B4ICAEBXgTBqHqT1AtAdTjrpJHrsYx9LBx54IP3yL/8y
XXTRRTQcDun9738/HX300fTIRz6SXv7yl9Pu3buJKHtv66pVq+i0006jo446ih71qEfRe9/7XiIi
Ov/88+m9730vfeUrX6FNmzbRr//6rxMR0fOf/3z693//dyIi+tznPke/+Zu/SW9961vp4IMPpic+
8Yl0+eWX06mnnkpHHnkkPfrRjx5xXZeWluhtb3sbHXXUUXT44YfTG97wBlpcXCQioksuuYQe97jH
0b/8y7/QYYcdRo95zGPo1FNPJSKiT33qU3T66afTBz7wATrwwAPp2GOPTXbPIE5Bp0BgBgDoMugD
mwfPAIBucMstt9DHPvYxuuaaa2hmZobOP/98evzjH08nn3wynXnmmXTppZfS9u3b6eCDD6Y3vOEN
I9+97LLL6NZbb6ULL7yQTjzxRLr55pvpd37nd+j444+n4447jvbu3Uv/9V//ZTzvlVdeSU996lNp
586d9PKXv5yOO+44uuaaa+i2226jz3/+8/TGN76R5ubmiIjoHe94B23dupWuu+462rp1K23btm0k
Tff++++nvXv30vbt2+nTn/40/dVf/RXt2bOHXve619ErXvEKevvb304zMzP07W9/O9l9gzgFnQIB
AQCgy0AYNQ+eAQD10uuV/68Iq1evpqWlJbr++utpZWWFjjzySHrCE55An/zkJ+mf/umf6PDDD6e1
a9fS3//939PXv/51GgwGPy9vj7Zs2ULr1q2jX/u1X6OnPOUp9OMf/zj4vE94whPoVa96FfV6PTru
uONo+/bt9O53v5vWrl1Lv/3bv03r1q2jrVu3ElHmgH7oQx+izZs30/7770/vfOc76Utf+tLDx1q3
bh2dcMIJtHr1anrxi19MBxxwAN18883Fbkgg2BAJdAoEBQCALoM+sHmQ1gtAvTTV3n7xF3+RPvzh
D9OWLVvohhtuoBe96EX0wQ9+kO666y76/d//fVq1atXPyzektWvX0gMPPPDwdw877LCH/73ffvvR
vn37gs8rv7tx40YiIjr00ENHfrdv3z7asWMHzc3N0dOe9rSH/zYYDGgobtghhxzycDmLlKUIcE5B
50BQAADoKhCnzYNnAEB3ePnLX06XXnop3X333USUpdEeeeSRdO6559LOnTtp586dtGvXLpqdnaXD
Dz/ce7xeURvXwKGHHkr77bcf3XDDDQ+XZffu3bRnz56g76csiwTiFHQKBAUAgC6DPrB5cP8B6Aa3
3HILXXTRRbS0tETr1q2jjRs30urVq+n1r389HX/88Q8L1h07dtCZZ5758PeGjk7isMMOozvvvNP5
GY3ts71ej173utfR3/zN39COHTuIiGjbtm303e9+N+i4hx12GN1+++3B5QgF4hR0CgRmAIAugz6w
eZDWC0A3WFxcpHe+8530yEc+ko444gjasWMHve9976M3velNdOyxx9ILX/hC2rx5Mz372c+mK6+8
8uHvaUdS/v8f/uEf0nA4pEMOOYSe/vSnGz+vcR2Pdw1+5jOfSQcddBC98IUvpFtuuSXoWH/2Z39G
N9xwAz3iEY+gP/iDP3CWIYZejPKug16vN2xbmcD0cOihRGedRfSsZzVdEgAAqJ+3vpVoZobo059u
uiTd5TWvIdpvP6KPfrTpkgAw+fR6vSgXEdSL7fn8/PdGVQ3nFHQKuAYAgC6DPrB58AwAAMAOxCkA
AADQESCMmgfPAAAA7ECcgk6BoAAA0GXQ/zUP1pwCAIAdiFPQKSBOAQBdBn1g8+AZAACAHYhT0CkQ
FAAAugz6wObBMwAAADsQp6BzICgAAHQVCKPmQVovAADYWdN0AQCoEwRmAIAugz6wefAMAEjHUUcd
5X3PJ2iOo446Kvo7EKegUyAoAAB0GfSBzYNnAEA67rzzzqaLABKDtF7QKRAQAAC6DvrBZkFaLwAA
2IE4BZ0DQQEAoKvAtWse3H8AALADcVqSHTuITjut6VKAUBCYAQC6DPrA5sEzAAAAOxCnJbnhBqJP
farpUoBQEBQAALoM+sDmQVovAADYgTgtCQb6yQLPCwDQZdAHNg+eAQAA2IE4LQkGmckCzwsA0GXQ
BzYPngEAANiBOC0J0nMAAABMChBGzYO4AQAA7ECclgQD/WSB5wUA6DLoA5sHzwAAAOxAnJYEg8xk
gecFAOg66AObBeMQAADYgTgtCdJzJgsEBQCALoM+sHnwDAAAwA7EaUkwyEweeF4AgK6CMat5MKkN
AAB2IE5LgoF+ssDzAgB0GfSBzYNnAAAAdiBOS4JBZrLA8wIAdBn0gc2DZwAAAHYgTkuC9JzJAs8K
ANBlWBiddx5Rv990abrJYNB0CQAAoL1AnJYEM6CTB54XAKCr8Jj1+tcT3X1306XpJogbAADADsRp
SYZDzIJOEggKAABdhvtAZP00B8YhAACwA3FaEgzwkwWCAgBAl+E+EBOrzYG4AQAA7ECclgRiZ/LA
8wKge9xxR9MlaA9SoIL6wb0HAAA7EKclwSAzeeB5AdA9fvmX4RQSjQpT9IXNgHsPAAB2IE5LgvSc
yYGfE54XAN1iOCRaXIQ4JcKa0zaAew8AAHYgTkuCGdDJAc8JgG6CiakcOKfNg3sPAAB2IE5LgkFm
ckCA2k1e8AK8MqProO3nQJw2D+49AADYgTgtCdJzJgcEqN1k+3aiPXuaLgVoEm7zSOuFOG0DiBsA
AMAOxGlJMMBPHnhe3QJtFLAoRT2AOG0DuPcAAGAH4rQkGGQmBzin3WQwgGPWddD2c7AhUvMgbgAA
ADsQpyXBAD85IEDtJggEAdJ6c+CcNg/uOwAA2IE4LQkG+MkBz6mboI0CpPWOAnHaLJjUBgAAOxCn
JeH0KDA5ICjoFgjCAZzTHDinzYN7DwAAdiBOS4JBZnJAWm83QRsFaPs5WHPaPOiTAADADsRpSTDA
Tw4IULsJshsA2n4OnNPmQdwAAAB2IE5LggF+ckCA2k0QCAKenMAkBcRpG8C9BwAAOxCnJcEgM3ng
eXULtFGAiakciNPmwb0HAAA7EKclgSszOSBA7SYIBAHafg7EafMgbgAAADsQpyXBAD854Dl1E7RR
gLTeHGyI1DzokwAAwA7EaUkwyEwOcE+6CTZEAmj7o8A5bRbcewAAsANxWpKQ2eeVFaLFxXrKA/yU
DQpmZ9OUA9QDHCJQ93tO5+baW+ekUG9rGacd9EkAAGAH4rQkIQP8Zz9LdMIJ9ZQH2EnhnqysED3+
8UmKA2oCQThgUVpXPXjpS4muuKKec8WCNafNg3sPAAB2IE5LEjLIzM5mM+mgWVKJ01270pQH1AMC
QVB3Wu/cXHv7fKw5bR70SQAAYAfitCQhAzzWvLWDFAEqnuXkgUAQ1J3WOxi0t5+Ac9o8ba0bAADQ
BiBOSxIywGOGuh2kEKd4lpMHJhRA3c5pm4UfxGnz4N4DAIAdiNOShAS+bZ5FB3HUvXYNlAcTCqDu
dtvmOieFUVvLOO1AnAIAgB2I05KEpvViIGqeVGm9ZY8B6gXtD9Sd1tvmOicnVNtaxmmnzfUDAACa
BuK0JKFpvXBOmydVWm/ZY4B6QSAI6p5Uartzin6sWdpcPwAAoGkgTkuCNaeTQ0pxismGyQHiFNTd
btu+zhnitFnQJwEAgB2I05LAOZ08kNbbLdouFED1YEOkHDinzdPm+gEAAE0DcVoSrDmdHOCcdhNk
LgCk9eYMh0T9fv5vUD9trh8AANA0EKclgXM6OWDNaTfB5BDAhkg5cE6bp831AwAAmgbitCRYczo5
pHgGSOudPBAIArxKJgfitHnQJwEAgB2I05KEpvXCOW0PSOvtFggEQRNrTtvaR0CcNk+bJy8AAKBp
IE5LAud0ckBabzdps1AA9VB3Wm+b+3yI0+bBhBkAANiBOC0J1pxODinEad1BLihPm4UCqIe6xVib
xQc2RGoe3HcAALADcVqSkMAXwXE7gHPaTdosFEA9YEOkUdCPNQtiAgAAsANxWpKQIARphe0C4rRb
tF0ogOpp4lUybe3zkdbbPOiTAADADsRpSUKEJ2ZJ20HK3XrbGniCcRAIAqT15kCcNk+b6wcAADQN
xGlJQtN6IWaaB2m93QSZCwAbIuVgzWnztLl+AABA00CcliQ0rRcDUfOkFKcQO5MDAkHQxKtk2lrn
4Jw2T5vrBwAANA3EaUmwW+/kkHK3XgQWkwMCQQBxmgNx2jxtrh8AANA0EKclwW69kwfSersHnle3
qTvjoc0TkhCnzQNxCgAAdqZCnJ5xRvZfE8A5nRyQ1ts94HQDIjinEqw5bR5MWAMAgJ2pEKc//jHR
ddc1c26sOZ0ckNbbPbC7MiDChkgSOKfNg5gAAADsrGm6ACkYDIh6vWbOHTLAwDltBymCATinkwWC
cECEV8lo0C6ape31AwAAmmQqnNMmO/qQQb7Ns+hdBGtOuwOcbkBUfz1o84QknNPmQUwAAAB2pkKc
NhkIhAQ9eM9iO0iZ1ovnORlAnAKi+tttm50xiNPmwX0HAAA7U5HW22RHHxL8Ypa0HaTcEAnPczKA
OAVE2BBJgg2RmqfN9QMAAJpmKsRpk2tOQ9N64bQ1D8Rp94DTDYjqb7dtnpCUwqitZZx22lw/AACg
aaZCnMI5BTEgrbc7YDIBECGtVyLLhX6sGdpcPwAAoGmmQpy2Ybde1yCPNaftAM5p94BDBIiwIZJE
3gO0i/pBnwQAAG6mQpw22cljt97JAa+S6R4IBAERXiUjgThtFvRJAADgZirEaRucU6w5bT8pd+tF
YDEZIA0bENVfDyZlQnISyjhtYAwBAAA3U/EqmSZnqUNfJYOBqD10Ka33058m2r696VI0BwJBQITd
eiVwTpsFfRIAALiZCnHapDOJ3Xonh5RrTifleX7hC0Q33dR0KZpj0iYTQDXU3W7bvM8AxGmzQJwC
AICbqUjrxW69IIQupvW22cGpg0l7XqAamtgQqa11DuK0WTBhBgAAbqZCnGLNKQihi85p1+sexCkg
QlqvBOK0WdAnAQCAm6kQp23frbfNgUqXSLlb76Q8T4jT7GeX7wHAhkgSiNNmgTgFAAA3UyFO4ZyC
GJDW2x0m7XmBasCrZHIgTpsFsQAAALiZCnGKNacgBKT1dg+IU0DUzJrTtrY7iNNmQZ8EAABupkKc
tt05bfPOjV0ipTidlMCizUFyHUza8wLVUHdaL5xTYAPiFAAA3CR5lUyv13tRr9f7aa/Xu6XX673D
8Pfn9Xq93b1e70c//+/vUpyXmYRXyWAgap6Uu/VOiuBrc5BcBwgEARHSem1MQhmnDUyYAQCAm9LO
aa/XW0VEHyWi3yKi7UR0Va/X+/ZwOPyp+uj3h8Ph/1f2fCYmIa13UsRMF4Bz2h0mbTIBVAM2RMqB
c9osmDADAAA3KZzTZxDRrcPh8K7hcLhMRF8momMNn6ss8bbJADwk6GlzoNIlkNbbPRAIAiK8SkYC
cdos6JMAAMBNCnH6GCK6R/z/vT//neZZvV7v2l6v951er/crCc77MKkDgVtuIbruurDPhr5KpssC
oQ5uvtn/zFLUkbIOzDnnEM3NlS9HKG0OkuugK4HgGWegj3ExaRsife97RDt3piuPJFScDodZvWK+
/W2ipaVqypSKhQWis85quhRu2jzBORwSff3r4Z8/++zsnoPq2bqV6Nprmy4FAGbOOCNtn1bXhkjX
ENGRw+FwrtfrvZiIvkVET7J9eMuWLQ//+5hjjqFjjjnGefDUGyKdcQbRrl1EH/iA/7PYrbcdnHEG
0Z49RL/2a/bPtME5PeEEok98gugZzyhehhi67py2ORBMyWtfS/S85xEdemjTJWknde6ynaKfOekk
oje/meglL0lTJkmoON2zh+hP/5TopS/N/v///B+iX/oloic/OX2ZUnHzzUTvehfR//pfTZfETpsn
zObnif7oj4he9rKwz7/rXUSPeQzRr/96teUCRN/8JtF99xE99alNlwSAcV71KqIXvIBo82b7Zy6+
+GK6+OKLg46XQpxuI6Ijxf8/9ue/e5jhcLhP/PvcXq/38V6v94jhcGicG5biNITUnXy/H35MrDlt
BzEOYZOvkqnbRe963WtzIJiSrjvkPuqsB6k2XquqrDHOqfz7JEyyTkI7aHOfNBhk8U8o/X63x5c6
mYT2B7rLcOjvO7TZ+J73vMf62RRpvVcR0dG9Xu+oXq+3joheTkRnyg/0er3DxL+fQUQ9mzAtQuoA
POZ4oWm96FSqJeSZpdytt+gx6hanXa97XdkQqeuTED4mUZxW9TxDxamuU5NQxyaljETt7Jf5/oWW
DeK0PiahboPuMhwSraykO15p53Q4HPZ7vd4biei7lIndzwyHw5t6vd5fZH8enkJEL+v1en9JRMtE
NE9Ex5U972gZUh4trsOFc9oO6hKnZQOLkNmllHS97rXZpUgJZtXdNJHWW+ZcbRSnkyBEJqG/a3Of
xGPTYEC0enXY59t+v6eFSajboLsMBi0Tp0REw+HwPCJ6svrdJ8W/P0ZEH0txLhOp15xWIU7bOBBN
EyHBXEpxWnSQqHuA6fqA1uZAMCVdf84+6qwHKZyxKp8nnNNmGQ6JVq1qZ5/E967fDxendU62dhlM
BIA2k9p4qWtDpEpJ3cmnTuudhAFz0om5x0jr7Q5tTqFLCfoYN3Wmd7c9rVefxwbEaTVMijgNAYKp
PiahboPukto5TbHmtHFSN9rUzmnXBUIdxKT1lj2P/BkL0nqLc/PNRNdcE/edLjmn036NZahzkiLF
uZDWW4xJ6O8Gg0ycthEemyBO20do3X7LW4gefLD68gAgSb3mtKVdZBypxR926508QoLzNqw5RVpv
cc48k+j00+O+05UNkep25CeNSdsQqcrJBuzW2yzDYZYy28ZywjltL6Ht77zziLZt838OgJQMBmmN
l6kQp6kD8CrSets4EE0Tda05RVpvcxRpR3BOAVG9kxQpNl9qi3MqPzMJE12TUEak9YIihN7r1OmV
AIQC51RRhXOaOq0XHXi1xKT1NrkhUt11YRKCtVCK3LsuidNpec5VMGnOaZvEqfzZ9jo2KWWcJnGK
DZHqIbRuDwZEy8vVlwcAhvsyiFNFk85pyIw8XI3qqWtDpBRpvVhzWowi19KFDZG6krpchjrrQapJ
sLaJ00lwySahv2uzc4o1p+0F4hS0ldhJrRCmQpy23TmdhAFz0qk7rXdSnNNpS+uFczpOFwR4WZpI
64VzWj+TUEasOQVFgDgFbaUK53QqXiUzGDT3nlOsOW0HMWm9Zc9T5lhI6y1OmTWn03IPTKRY4zjt
NJHWW3bNadMbIkGcVsO0pfW2/X5PCzHiFGtOQZ1wvYQ4VaQWp0VSRLHmtFlChEtbdutFWm8x4Jya
6YIAL0udAj6Fc1pXu43ZEClmF/ummIRMEaT1giKEtj84p6Bu5BiRiqkQp6k7+SpeJdPGgWiaqGvN
KdJ6mwPi1AzSev1gQ6TRY5v+bfscnNO0tFmcYkOk9oK0XtBW4JxamIS03rYPmJNOXWtOkdbbHNgQ
yQzSev3UKU6x5rQ5JqWM0yBOuY62/X5PC0jrBW0Fu/VaSO0OVZHW28aBaJqIWXOaQpyWcU6R1luM
MmtOp7n9dUGAl6XO1Odp3K2XxzBZpne9i2jXrmrKWJRU9+2MM4guvLD8cUy02TnlsSkkyOTPTsv4
0nbgnE4Hp5xC9KMfNV2KtMRmXIQwFeI09UCO3Xonj7rEadlj1F0XpmlipExa7zS3PzinfuoU8Kk2
RGqTODXVsTPOILr//vTlK0Oq/vXyy4muvrr8cUxMy269EKf1EhqXQpy2m4suIrrxxqZLkRY4pxaa
dE5D03rbOBBNE3WtOUVab3NgzakZiFM/k5jWm7qsc3NExx6bTpy2sW9JVaYqUyM5rbeNQJy2F6T1
Tgdt7DfLUoU4xZpTA3BOJ4+QYC5FsJcirRfitBgQp2a6cI1lQVov0d69RD/4Qbw4lX2WLFMbN8NJ
Jer7/eoC/Dan9RYRp22rA9NKqMkB57TdtLHfLAvSei2knmVOvVvvNKVWtpVJSuutumPatYvozW/O
/q3r3oknEt16a7Xnr4oiGQhdWI8J59RPnfWgrRsi8aRrkd16uc+Sn2/jxNckOKdtFqcxghPOab1g
zel00MZ+syxI67WQ+mFXkdY7bZUxhn6faGam2nPUJU5jhcCuXePBYNV14f77ic46K/u3vi8XX0x0
xx3Vnr8q4Jya0XVyz55u9zcmUjinoZv/tHXNaaw4taX1Li5mKcJtHNcmRZxizSmIJbRuD4cQpz6a
3Mitjf1mCK57xtcDcaqowjlNndbbxoGoLs4/n+h1r6v2HDHBXJ1rTl/yEqIbbhg9d9Ud02BAtLSU
/7vtqXihlBGnkzgYhKLr5B//MdEllzRXnjaSYpLiiU/MhFkd56oigDEds4g4/dSniP7hH9oZZKUU
p1UF+LzmtI0xAcRpe4nZEAlrTt087WlEO3Y0c+429pshPPGJRAsL5r/BObWQ+mEXEaeuz9e9zrBt
zM9n/1VJW9N69bXXkdYrxamue3WcvyrgnJrRzmkd7W3SSJFqOzMTNvhOS1qvrFdSiHD9amOQNSnO
aVvFKdJ62wvSetMxO2sXWlXTxn4zhD178rhSU8Wa06nYECl1Jx9TceCc+qlLkLUxrVc7lXVMVPT7
+eCk6x7E6fShxdAku+NVkcJBD92LINUkWOo6y+JU7hRbxDnl+tXGICvVWIu0Xv9nsSFSvUCcpqNJ
w6iN/WYIrk3isFuvhcEg/W69MecmwppTF3Vcf0hQklKchh5DX3vTab2TLk6xIdI4Wnh1vb8xUWeq
bVudUy5/2d16+b82ToLI51wmJqhyt16k9YIixPQ/SOt102Qc1MZ+0wePG7Z6xfUSab2K1LPMMcEd
duv1E5MmXZSQYC7FM4h1YJoQh6603knsGBk4p2a0mw9xOk6KXbZDv5/Cpa3iGabarVcK1LbVs9jM
FtdxkNYb9tm21YFpJTRzA86pnybFaRv7TR98r3zOKV4lo0j9sFO/SmYSK2NK2pLWy9TpnDaV1ruy
kp8Lab3T3f6Q1uunrGiJ+X5bnVMpTtlVnMa0XvmzzHGqFqdtBM5pe0Fabzqa7Lva2G/6CBWncE4V
qQfyGKcvNK3X95lppq603lDntM41p02l9RKNpvbKv02qcIFzagbOqZ8mnNO2iVOZ1sviqIg47Ypz
WvVuvUTt65cgTttLaIwzHEKc+hgOu+mcXncd0Te+Ef89Fp1I641Eu0MpjhfjwvV6EKcupkmcxh7D
lNZblzjl115MU1pv7LOrSpy++c3tac8Qp37KOugxgXid61tjkNdQxjntijit0jkNuf9NoMXpli1E
O3eaP4sNkeolJsbBmlM3XXVOr7iC6Oyz47+HtN6CVJHWGyNOfetHuuDeuKijMcasOW16Q6SqB3M+
PovTLqf1VjExNBwSnXxyewIAfY1tFA1NU7YexHw/hUCqardeonDnTqfy8r8hTsvR5rReLTi/+lWi
e+91f7ZtdWBaCWlv/Hc4p26ajIOa7DeLxp8+cQrn1ELqgTw2rdcnTlMNmJNKHR1BjKtWZ1pvE2tO
+fj8Hi+k9aYXp1yeNqDLM8nueFWkSuutyzmtKq2XKKsbMeJU79Yr15y2rZ6lau9V79bb6/kzrppA
O6euPhfitF5C4lKI0zCaTOutY4NQG0WFsS+ttwrHHq+SsRwvxjn1vbOs62m9dTTGmJSXMpRN661T
nJrSetvi+qw4AAAgAElEQVQYUIZSRpymzqyQP5sGzqmfVGm9Mc5pW9N6U605bTLIsjEpzumkiFNX
EA9xWi8hE/BVOFjTSNNpvU26tlU6p0jrVVThnMa4cKFpvV3txKcxrTfGWa9bHLrSeifBVXvOc4ge
eCD79xvfSHT++dm/Y9xxpgrntIpMiF6PaN++NOWBOB0Hzulou2dx6jqHHLfwKpl0cMzQRnGqg1DX
M5afAdWDtN50lInD/vIvif7jP8qdu8m03iLnxm69BUn9sGOOF5PW27aBqC7qSuutU5yGHgNpvfHc
fjvRnj3Zv++7j+ihh7J/tyWtN7VzWnbWUQfkkzABUTch/bSLup3TKtN6ico5p3iVTPljT5Nzir6m
HiBO01Gm75IxSd3nLkvR+K+JtN6JEKff+AbRWWfZ/97kmtOYtN62DeR1UUdjjE3FLnOemGM0kdar
ndNJE6dzc6MzdSHrn2xUMTGUuj3PzZX7PtJ6/XA/XfS+FHFOyzyDKtN6icqn9bY1pTOlOK0qwJ+k
tF5XPWxrHZhWsOY0HWXWnJaNoSbZObVdd2fTeq+6iuhHP7L/PfXDLrJbr+vzg4FfwKZiOCS65ZZi
373ttmo6tbaI01Tpdny+IuWqy0UmmtzdeufnR2fqyojTSXBOZ2ezn6mEU1vEadF+qApCll+4iJnk
SNXPzMwQ/dmfjf5+YYHozjuLHbOMc6rbYFtTOifBOW1zWq9JnHZ1zekDDxB95zt5BlLTxDinWHPq
pswYWTYzaRKdU6T1Wlhedt/Q1M5pTOUJSRcrO2sfw/XXE/3v/13su0cfTfTpT6ctD1E9giikDiCt
t/0pn/3+aHtfWRkNOIuuOU15z1M7pyxOi9ZLXa/b8Iz37CH6jd9otgwSniAsE5DwcULORVRenO7Y
Mf5OuvPOI3rDG4odM5VzKneybZswSTUZVbU4batzqifeXOPVtIvTD32I6Hd/l+iii5ouSQbSetMg
x8kilBWXTYvTIuf2pfVWMSkyEeJUBqgmmnZOQ9J663JOFxfLdUxVDMht2623yQ2RkNbrZn4++5kq
rRfOaTMsLWX/tYWQftpF3c4pp5XqezgzQ7RrV7FjyvrKu9uH7pWg6xaPMW3rS1JNHOFVMvn/d9U5
3bkz+9kWoRcyOQtx6qesOC07+dvk5HHRdOZQ5zTldU3Eq2RCnNOUVCFO16yppxOXwXwRNm1KVxam
LWm9KeBZ7zavOZ3ktN5JEKepnVPepXeaxGnZfig1qdJ663ROl5fzNszMzuabhcUSm9ZrWsPM/RcH
v03XM82kpPVOijgNcU7b1M5TwpNAbbk+pPWmoWwfMelpvZPinE6FOOWZyFTEpA+GBD1lZ+1j6Ko4
DRF9qRyNNWuKidMqZpds5ySaTOeUNweSnWEZ0TVJzmkqV68t4rRNAVKdab0pUsmHw+z+mcTp7t3F
jlnUOZV9Btettqb1Too4beuaU923ddk53b2b6IAD2jNeYkOkNOgJmCLfn+S0Xqw5TYgvrbfJ3XoH
A7c45d/7Nk1KRVFxyuljGzakLQ9RPYKozrTemCBXzrJVsf7Rdk4iszhtw3pEFz7nNPbZpXY5Xcf8
4Q+JPvnJ+OOlTuttwzNuQxkkdW6IlMI5ZXGkRVIqccoUXXPaBee0qgBfTqa3TZya0np9zmnb6kAq
du0iOvTQ9vRjMc4pxKmdLjunZXfr9TmnndutN8Q5TR18hh7P54qyeK1rltR3r2xwqlgVjaaOxliX
OI11wXVgJ39WBR+fN0Sa9LRenVIYQ53O6QknEL3+9fHHm8Y1p21z1spmrxRxTlOk9RKNrjudnc3a
SJH1vFx2TinVZdy2jWj//cc/r/swOKflkGm9bUMHma41atMuTnfvnjxxyu0Z4tROijWnXXNO8Z5T
Cz43sEnn1Dcjz+K0Tue0yHl4Nr6KjrgucVrXbr0xzqm8dqT1+pnkNacHHljseLzmNNVuvW0Sp22p
ayxOy04A1LUhkhSnMrWXJzKKrDvlZ2ETp6ecMvrO3UlM652U3XonKa3X55y2pY2nZtcuokMOac/1
xTinbVpS0TZSpPXCOR0/ruvvRZgIcZrKOX3Vq8IG9dRpvXVufhCS1nvppUT//M+jv+P7UkVHXEeK
X0yjSyFOQ4NUOfPchrTeSRGn3MnJtt8WcWoLyoqu1647rfeEE4h+/OPxMvzRHxU7vwnfTGvdxLRb
2/flzzKf/dzniL7xDf8x+N6ZxOlTnkJ04YX+skh84vTLXx4vA3/Gltbbtr4klXOK3Xqzn111TgeD
LCY65JDxevCKV+QTinVSds3peecRfeIT6cs1aTSd1hv7/Q99iOjii4ufT1I0/kNar4WQNachFe3C
C/PtwV1UkdbbpjWnt99OdPXVo7+bBue0bWm9tnTeJtN627YWUONK622LOLU9x6bFaahzesUVRHff
Pfq7PXuIzj+/2PlNTJtzqieYfOdyffYnPyG66Sb/MVzO6X33Zc8xBl9a78yM+fOmtN4urDntonOq
g8wQ57RtdSAF+/YRbdxItH79eB/23e8WX/ddhpDsMJ74MInTW2/N+p6uk8I5rTOt99pribZuLX6+
Mudmmkjr7dRuvaGbBfX76XbrZXGaciDi45iuOeQaB4NcuDBdEqdlzxMa5OpAqe60Xn7Gk+Scclph
mzdEsjmnRdN6U+3WGyril5bG/y4FRwraKE7b8iqZkAki15pT5hd+wV8WfV4iuzjV44mc7JCCu81p
vZMgTquICVJhEqdddE537SI6+OBsrNfX39QEb2ha7/r15rrbZDppmyibwVb3hkgpYzZXJoSLUOe0
c2m9IWtOQx52jDhNndab0jn9yleI3vpW899C1pwOBuOvKGBxWkXn1TZxWldarxYxbUrrHQxyl7JN
TPKa06ad07LitMgmOzbaJk5j2q3t+0RpnNOQ4EaKI+2cPuIR2b9jd1aX5zSllWpxanNOZcpr24Ld
lOK0yt162ypOTWNWF53TXbuIDjpoMsXpunXmumvam2VhoT1LL+oixjldXh4fFydZnBaNxbHm1MLy
svuGhjoqoeI05gE24Zzu3m1fOxvqnNrEaVXOaVvWnJZ9DjHpgTbntA6hTpQ/Y9Nuvd/5DtFf/EW1
5SiCXnOaIq23jGNmwuac8k6nsXWd1y+VFafSmXeVoU7ntC2BT6q03jqdU5s4fcxjwstiKhcLU90u
dP9kE6eyrrRNmMA5LQeXLcY5bcsEVEp2786c0zVrJk+crl9v7stN33/b28bXmk87MX3EyScTfeAD
498v079MonPqG89jBH8oEyFOfYIr9GGbjnPbbeOfi3FOfUEPd/bsnPb7RHfcEXZsGysr9kGtaFpv
lRsi1eWchuzWW1aoDAbZgDVJa07l+XhgnZlpZlMHH1U4p2UcMxO258jO0969ccdrIq1Xn4u/k6r9
t805TZXWK79vGjvkZ+QzuOuu0XsSk9arxekRR4wfPwSd1ltGnLbVOW3Lbr0PPZS5b7Zjt3lDpHXr
Rp+v7RmvrGRjYdvqQAr27CHavLldzmnohkg2cWpyTvfubWccUCUxy6v27h1dSsHfg3M6SqedU19a
b6hzKm/ezp1Ez3rW+OdiHqAvXUwPRFdfTfTKV4Yd24arkwp5z+lwOO6ccgdVRacbI/aLEvLMUonT
ohsi1bXm1JbWK3cPDs0iqBvfhkixz65O55TPoTeW8VE2rdckKlzHWlwc/ztfS6rU3mkVp/K+HX00
0YMPms8lfxIRvfa12S7pROXF6e/9XpZCXpU41S6xnG3Xzmlbni+TagKQx6yix3nyk4me+1zz39q8
IVK/T7R27Whar8s5Xbt2OsXp8nJ2bW0Sp6HOqZxc0H/T9a2pa2mSGJfPFLuWjWdj73lRt9NEWXFq
KwfrnM6JUxmg7tlD9KMfjf69qHO6tGSeYYp1Tn1rTqVzasphj8VVvqJrTqtcP1J25mfv3vHdhTUh
ab28/rdsWm/o+uGm1pzy8XVarww+2ypOfRsixd47zlxIec9tAbDso2JIvVtv0bReonSpvW0Tpzyp
VPQe6zbMyPeCynPpz8p+P3bNqd4Q6aUvJXrJS4q1BSK7ONVBm8057cqaUyLzc7r8cqI3v9n9/Yce
Itqxw37stopTFjchfe40i9N+P3OF2yZOh0Oi44+37xY8GNifiSlG6rI4DY3hTGPlpDqnVaX1Doej
k1opmAhxKt3ACy8k2rJl9O8hzik3bHnzbBVP/vThSxvUA1GKWRCfOC2S1lvl+pEyM9BERN//PtHf
/V2ac6wqWeMHg/an9fIz1Gm9MuBqqzg1rTktm9Zbt3MaK075WutM67X1e6md07atOU3pnBKNT/Lx
ueRPotEgsKxzuv/+xSZctHOq74cWZHIyTQpu6Zy2TZikFqem+nv++dlaNN85bBukTZI47apzurKS
tQ8tTrn+N+mcfu1rRNu32z9jWifLf5tk53RubvwVaEWIdU5T37MmxWlZ59QnTjvpnPLNmZsbvwEh
N9w0k29yGU2z3i54oPGJUw4m5Ix4UVKIUx1UsS3fRnGq07GLniOFcxrjwOhAqa60Xg4wdFqvDI5D
0r+boIr3nNa15rRoWm/ZgFrWL/6vqDidVuc01YZIuh6ZxKmpj5D9fqg41Rsi9fvZs9u4sdiEiy+t
1+Wc6gmirjinpnHnkEOyn1de6T7GJIpTndYb4py2pY2npN83i9MYYVNFmbjtudIrefJc1y3TuBAS
W7WFc87JNnAqS0wGm00jlOlfJtE59YlTduw7J07lbr3z82bHwtfJm4IlWz45UZxzGvIqGR6IUlQ0
V+puSNBgEqf9/uiMaUrKXnNoGlyIOC3rosWInSbTejdsGE/rnRTnVM78ln3PaRXi1Oac8v2NdU5T
iVPZBnxpvaYNkfhvKWibOPVNIoZ8X/5kTPfL1M/IPrCoc8quadFXk/HnXeJU79TKP7VQTSUCU5Na
nJoma3jDM15DbOOAA+zH5gyetolTDjJlHXA5p+vWta8OpMCW1ltlhpkPbocuc4Inxkz9w6Q7pysr
aSZPY51Tk0bomnMaktabWj9MhDiVAer8fDnnVH63DnGqnVM5I14Un3PK57UxGIyn9fKgJL/30Y8S
3Xuv+Rjnnkt0ySVh5a3DOQ2ZoEjpnLY9rXf9+slN6z3ggLyOmzZjiaGKtF59P9/whizdqGhar3bW
y5QnpI65nNNzzyW64IJi5ZD4xOnf/m3cq4wGg2ytVVFCJil27SI66ST7+fk4EpdzWlSc8vf0mtO5
OaL99sv+HSNOL7ooS0UNcU7lxJCtXmlHuEoeeojo//2/8M+bUqqL4HJOZ2ay52t69pJNm7KNBt/5
ztHjDAb5M6iKSy/NXhdmYts2oo98xPw3LU5dWRhVpvX++MdEX/qS/e8/+QnR6aeP/u6TnyT61rey
f99wA9HnP1/8/DKtV8eM8qfmM58huvXW4ud1IbMWXM4px5smE6eI0PrgB/ON377xDaKrrjJ/7tpr
076W5sYbiU47Lf9/mbFh47TTiL74RfdnqhSnl16aOby+8w8GWWr2ySf7y+ASp1ddRXTGGf5jhBzL
BZxTCzIFcW4unXPqSuuNEacxa05TzIKEiFNf8GNyTnWKzpe/THTzzeZjfO97RJddFlbesuI0lXNK
lG633pBz6brUlHM6SeJ0eTlLW5SzpLbAOARufynvuQ5QPvEJoh/8IH++se5j2UkLGZCXFaff/W74
pJMLXz/0hS8QnXJK+PEWF8ffNxdDSFrv7bdn5TKhBRvfcz3Jx38zCb/QtF6bAF5ezmanieLq9CWX
EF188eg5bbv1ateMf2+bIKq6D3E9ExOpJgBdwdjevdk7MH3XvmlTNkaedBLR+9+f/57rR5VpvZdd
lo3RJm6+OVu3aGIwaMea02uucQf5//VfRGefPfq7178+T/u89lqis84qfn5bWq9PnH7zm0TXX1/8
vC6kc+oTp6aNnIo6p1/4Qv76w/POs6ezX3NNNrmZimuvHX3GISmpf/InRK94hfszMXGYKdZ2xSE/
+IG93clj9vvZJMZXv+ovg+u6r7wyG7ND8S35sRG6IVKnxakprTfGOU2d1sudgUucyjQsV0X7n/+T
aOtW/zld4jRki//BYDRVmn+nxenysr2yxaxV6PfDJhBc30+15rTOtF6bOK06oGNxyiJJn7ffb++a
U5lerttsG51Tbm+PfrTbbQk9Xtny+I7FE3I2cTozk2aACZlpjYEnU8q4y756oPtE/X350ydOyzin
ugxykonTQWPEKffj/HnXhkgmcdqkcxq7Ji6VOPU5pwcf7C/XAQcQXXEF0S/9UvZTHrtqceq6b65l
QXKS2hfEVylOfWO+bXL1wAOznyEum+/8RdJ6q1zDyfGj6/n5xKn+Xkh55flczyXkTREx6OOFPFN+
/i5inFPTNbn675j9UULHM5ehFVvPq3ZOO5nWyxXElNabcs3pYBD3YumQNafaObU94B077C/ulrgq
dYhzytcm3VMpCphU4rRswBC6yVMd4jTGOdUDWarAKeS8a9fm4nSSnFPZyekUddPMr4+q15xy2rsM
NIuI01Q7yfqCJ10n9DH27k0TXPn6odiUxrJrWEPqgclRZrQo5f83iVNTH6EnW4o4p2XFaUhab4g4
lWWfZnG6fn0x55Tv6QEHEP3wh0TPec74PWtSnLomt2Ud8AXxpmyrVBQVp5s3h33fB6f16p1vfQ5S
leKUn0mIc2rqH0xxcohzKuPvopMeRTCJU19ZDzoo+8nrwk3E9BE2A8s1+et6/vwMuE8NKUNqcVrk
GfX79v6QCM4pEaV1TldWzI117drwQSM0rVfu1uvq7EM6el/j4PPasIlTPQvqctdCyyrPV7TjCjlX
SLoCrzktQ4yQsLktVQd0g0E20TCJ4rQK57TK3XrvvDP7t5wwir2vsRNitvKEpPVqN10fY2YmTb3w
icnYtuAT3T5C0npdzqkWbFx+3l1an8u3IZIvgJHIdlynOJXPyFTH+G9VEjPOEKUVp+vWjT6nV786
Syf1Oaf79mU/V6/O1k4+/en1i1PXffOJU+5/ffeS++oq6oBPiNiuj8VpUYdIHr9IWm9sfY2B22FK
5zSkvHqioki9KoI+XogQ4+d/4IFE991n/oxv0sVVBv5+0ecv+9TQ++U6X0iqc5nPMysrbnHKY0fn
xKlvQ6QQ55TT7/Tidv1dTucIbWTcGYSIUz6Xq2KHPFxX51TUOdWBCVG7nNNUab1lA4JJSetdvz6v
86a03qrFqclRCoFn6FKK0yrfc8riVM8ux2By2mK/zz9DxalpwCVKl9br64f496Hn8jkWPkLqQWrn
tE1pvTIQKuKc2tpg1eK0Sed03brR3UHvuCPLbmLn1FYufpXUYJDVj82b2+Wcxqb1+pzTKupAUeeU
0zrLOqccB7YtrZfbos85NYnTFM6p6762wTmVab0ul4+P58PmnBZ9/nqsbiKtt8gz4okon3OaMqac
CHEqZ7T1hkhyMxDXg7al9cpjEMW7GD6xwoKo1xud+TIR2qGGOKchwY8MrKRjxaQWp0UrbkgHGtro
upLWKwMrk3Na5ZrTnTuJ/tt/K/Zd2Qma0npj7x0P1invuSyPFKdl0nr53XRlyiMnvmzPtm5x6urr
XH+PPZ4Pk2DUxDin/NPmnJrEqbyGkNl1xiROeTwJweacmsoYsluvFlpVEhvsp8pO4Qk+eW4Oln1p
vbxbN983HbQ1LU59zqlO6/UJ2TaJU+mcpkjrbaM4dfUfUpya+nj9u5BJ6raIU15v64LTeonsr52J
iUdtzqkr/o4RpyH3K6U4Leqc9vvZPiYuceoSr0WYCHHqck5lqmasODWlwMZ2uL50Me4sUjqnZcUp
36cQ5zRF+kpZURbS4Ye45+yerKzYX5HjIyTIlZ+VP7uS1js3F/86FUbWw0lwTvm1AT6nYTgkuusu
8/FiJ8RMx+bj+NqaT5zu25emXoQ6p6Hniv28JiStN5VzajqXDDBCU7+Yutac6tlvec1ykkePl1US
M84QjT+nMufVwRYHy760XumcmsZVOWHdRFqvLy00ds1pVeLU9dz133mSiHezjq03puO3La2Xxxjf
5ILrVTIm59QXW8nzueIGV7mIst135athfOjjuUQaw5MTRPZd82PEqW3pX9HnL/tW3/1iXJoh5J7o
zxdpr0jrNcA3U4pT0yykLwB1Oad6sK0irVc6p6nE6bZt4+dNveY0hXNqus8xpHJOWahcfjnRH/9x
sbKEBLmyTPJnFWm927ePH4/FqU7r1eK0KpFc5tjSwTeJ09hgruo1pzfcQHTUUfk12zron/6U6Hd/
1368tqT1EnU3rTfVbr2mMUH2Yb7+TJfBJk5D63RIWi8HrjbnlIN13c9WPdEWOs7s3Ek0O1t+IpQZ
DOp3Tu+/3xxQr6zY18/ZKOOccv/rm0yVfXVqQpxT+fedO/PvEcU7Sqbzt8k51ZNILrHCWRGmuEA/
y5DYKpVzes012atoQjGl9fruLU9OENnFaRvSevm4TaT1FnVOQzZEStkXtF6carFlc059aU6h4pQH
kxAnjs8f+ioZnoF2DRohD5cr9stelm3QICma1msaRNuS1htyrlBx2utl1+17gbrrPKEpmHogq8I5
fcUrsh0h9XnlrL++//1+tWm9ZcWpXnNqEl+hVCFO+b4tLRHdckuWwswzrDZx6qpzLE7rSOvlMuhz
NSFOY2ZaU6X1FnVObW04ZkMkeU9CndP16+vZEInLLINa3e540lYLrSoJHWe2bMlcmZTi1OScLi9n
z3zzZnu5eEOkWHF67LHmdxZeeCHRa18bV/6i4pTbZahzWtWGSCHiVJaLxalsY2XTetu05lSaMK7z
y3asn0vTa04XF+PujUmc+sqq41cTMfGoqa244pBJSOst0l77fXdar2tiviitF6f6vZ1lnVM92PAx
GJ4xI0ojTvnvLJ5TpPVyo11aGg94Q99zShT2Kpmi6Qum81XtnIZMKHDnXjbILZLWmypwkszPj7s3
POtvKwfXs7aKU73mVAbLRcRpVe85veUWosMPzzZh4EHMNnvoatsy8C9TnlTOaYp64ROT0qEJwRcU
+giZpIhxTk0TfPKzZTZEkt/bb7/0ab1E4+KUjy2DcZ0uzpO2OmCsktBxZmEhczSrFqczM0T77+8O
xGRcESpOH3iA6MorzfVpZiZ+gzlX/+5L6+Xr9k2mrqy0J63X5JyW6cekcyqfs68fiomLYtDi1PX8
bGm9pvEzJA4IzfpwTXoQxYtTfbyQNaeybL603pB6ayqDL4YPib25fpYVp7FrSIu2C19ar2tiviit
F6c6QDWJU54J/vzn/QNGiHOqxe511xH953+aj+sTK/p4rsohA9hLLyW67Tb75/g4+lhFnVM5Y8o0
tVvvz35GdO65o2XznUs6ACZuvDEb/Hl9ctn0wNBORf60DfZzc0Rf+1qx8pieAwdEROMBKFG8OF1e
JvriF+PKVHSAlsFcCueU21/KAIqv7Sc/IfrVX82Epc85ZdfFVsbVq7M1qd/7nv2827YR/cd/mL9P
NCoc5PWee27WpojSpPVecEGWTu4ixDl1DXa246VI673ssnytsCRmzSn/jNkQKVScyjJIcdrvlxOn
/HnThkg8jpqc0+uvJ7riinwCJUac7t5NdMYZYeUcDok+97nR33H/dtllRFu35r/nZ8h958pK9ixC
xpq77iK66KLR3115JdFNN+X/zyJNttmVlex6Nm3K79PS0njfGCpO+ZqJ8nRHU/2enXXX+wcfJPrW
t/Lvn3qqe8x0BcVy0sjnMHHMUIU49TlCeox56KH891w22/cXFohOP330d9u3Z/0aI8Vp087pYJA9
0xDn1DTJxBRdc2pyTk0xSxHnlNvd4iLRl7/sPl6IsJLHT7XmlM/7mc+Y+8Zrrhn9fIxzGmpyrKyM
943yb6GUcU45o81WRs4oTNUftF6c6h1H5+bG03q50b7lLUT33GM+Tqg45U5JDv7Pex7Rs59tPm5o
Wq90Tm2VUnYUn/1sls5jot/Pj2OaCdPXaSoTkXlDJHm8psTpFVcQffjDo+cKcU5d5zjzTKIvfSnv
3G1CwYdshCGflT9ta05/+lOiE08sVp7l5fFrYfeRaNSRKypO776b6P/+37gyFe2gpINvck6LrDmt
yjm9/36iRz86XJz6nNOLLyY65RT7eb//faJPfMJeHtkfyPv/4Q8TXXVV9u8U4vRjH8vEgYs2ilNO
dfvUp8zpk0V263U5pzqwKpLWu2HD6BhY5lUyfE5TWq8pqOXjf/vbRF/5SjFxevnlRG97W1g5+32i
P/3T0evndnPqqaPP7NRTsz79hhuyvnN5OXsWIUsnLr6Y6N/+bfR3p59OdPbZ+f8PBuY1p/PzRBs3
5m3+nnuI3vGO0WPJ5+USp/Kd2+ecMy6Gmbk593j1ta8R/f7vZ9d+3nnZ+1hd/Y2r75f9r29M5c9W
IU59oklfA6/zlRMDtu+feSbRK185+rvLLiP6+MdHz9+WtN6ZGaI///M8LnWd3yVOTfFiiNMrRSJf
H7c72+dMLC2N35vTTyf6zneIbr+d6G//1n28ECHW7xO96U1ET3uaf81pSPzD7eCuu7LUei1sv/1t
oq9+dbTMoeI0xjmdnc36Rn1NseI0ROCb6Pf9u/X2eqN7FpSl9eI0xjldWsrXe/iOI3/nE6eulJrQ
tF7pnOpyyHPz713CkCu1qaKZrslUJiJ3Wi+nULjKEFoJY2aq+HNyMA6Z3dMCUMMBWlnn1BR42tAD
mW2wNwnMUGzOKaf1yrLK8sSsOZ2djSufb5ByIWfodIq6aXD1UeWa08XFLPDk1C9TIMqEiFPfwGb7
uwzITcHT8nL+mRRpvbK+bt9u3oU4RJwWSest226HwyzYM9XnIrv1xqw5DXVO9ZrTFOJUBvOxa065
zvDkpR5/Xdx7b/a6Jdu4rMtJND5Gm/qrxcXMLZufz69POqe+9G393JaWRusEO4hanC4vZ/eJg7Dl
5YuQigEAACAASURBVPGAcWUlfz6mjCS5T8ZwmB3jgguInv/8Ys7pox6V/bzxxnxC2ydAfc4pT7bx
500sL7vdlDL42oj++8xM9hqRkDbGr/+S6Pq1spK1BR1s+8RpSKwSC9fLmLTelGtOZX3hz+s4XH/O
xOLieL/LY4mpHenjhYrTY47J2oRvzWloDDcYZBksRLkWkHG6rh8xzmlIGYbDPFbn9HV5vJj2VySG
IsquyZfWy/UuVf1vvTg1rTm1OadSnH70o6NpOqHOKTfuEHHKDT12t15dDlkeLmdZcRrinLo2RPId
J2aG0HSfXaysjHZUIS6fb8acXZGya05jxI7NOa1anErnVKfu8d9jnNO6xWnK95xWIU65DCxOOYAp
45xyp+56JrZjyPplGnilI8jtqsyGSLK+fu5zZjfX5XRyOWPeixbSr7mQgnHPHnN9jnFO+f65XiUj
77EMAn0BoSxDCnHKjgV/PtY55Tpj2q3X9zy2bct+3nijv5wmccr3yiROd+60i1PXvQkRpzxJZhOn
3F5t4lTueKsnYWRMMBxmqY2PfzzR4x5nbg86W0zD13LBBfmyAFeQHCpOffeSA9Y2OKczM0SPeESY
c3rHHeO/022fTYoizmlqsS7FKU+u284h41f9GdP46SsvmxQ6dtBxOB/LJ071d1zi1OSc+u4tTyrI
V+lpYswSbivcT7I45GOYJjV8kyqm47oYDPJxxiROY2LZkMwSE/2+f0Mkdk47I05jnNPhMBen55xD
dPPN48eRN84kmrhT0oP/mjXjZeMH7Xpfmews5MyV6QHKDtmXlmObeYkRpy7nlDtEVxlCK2HMTBWX
RQcKvo7Ed46lpewYTW6IZJuJLpMKZBK2HGAQjaf1spCKFacx5SsjTuUkia7LRcVpVe85XVzM7mfZ
NafDYTnn1CTetdjUQsPlnPqetSyHrW26+qEiA5lL7IYg03pnZszHSeWccp+vnVPfPZNlZWRAUKVz
ahOnq1bl40SRtN57782+d8MN/nKa6gz/bmHBLE5ZuHFaL5fZVa6Vlex7EplyyOO0bstc79k55f/X
QfDycj6WmlLdtDh98EGixz42+5ypj/BNDvK13Hsv0a5deRl88YMJOTkY4py2Ja1Xv3vW9X2Tc6qP
1++3J62Xj1d2zalJDMU4ffLzpgmTIuKU75epHenjhW6IFCpOQ+otl4HvG69tliaO7q9C76fPaZbf
SSVOY2NxhieibOfiOKtTab3Ly7nr2O+P561L55Qo27GPv2ca5Ey/CxGnGzaMl43P7ROncs1pSufU
FOQUFacsCuSMkDyeRjfKb32L6Pzz3ecLrbS6owrp8H2Nju9nijWnZdJ6Ta88qiKtVzqn8t5I4ddm
59QmTmNFZkiwGotsP21I69UDHtFoGUzOqb4fpgDMhqyvtgkDVz/EfWzMQKYzOmKRk0pFnFPdv/DP
UOdUP5tQcaqdU95J3vfqtA98INvIj69LntO2IZJJnK5Zk9eZIq+S2baN6FnPKu6cSnEqn/3Cgj2t
17fztc855bRbmziVjprN8eFAziQUtDiV7cFUv0OdUxkzLC7a65jPOeWyh4ypVTqnviwSk3Mq667t
+zFpvbHi1Cf2ipAyrdfU74c4ffw9vu+mtN6yzqlp7ww9ERbinK5Zk7XdlGtOuRxanJoc91BxGjrZ
PhjksTqfX/4tRgzGxuJMv+8Wp0UmnH1MhDjldQ3z89kNsDmnRLlzqhuKKVgyOad64GBs4lTPQN90
E9GrXjX6mdTOqWwwupLpDaRMmAKrfn80sPa9kkY3wh/+kOjqq93n8zXEv/7rbFfkos6pS4RwJ5Ji
t94yzqlp0Cgz22r6Lgs8otGySuEXuub08MOzzblinVPT+pYQuBPk+qWd39jjVr3mlJ3Tfj9NWq/r
PtvagaxfprYm+0L5WhLTMfjzLlI4p65g3HZO2/FCKOuc8nlDnVPThkih4lR+TwYE3McR+SdcLrkk
3+3dtluvdk71br3s6PNnirxK5t57s/cAh6w5dY3RNue0iDjlz0pk4Mz3WddPm3NqijXYfQwRp/z/
tr7Dl7kyP5+93kaKUy3m9fW7xI1O63W5hE2l9eo2FOOc2tbIm0yKNqT18nXEbIhkS+uNXXOqDRy+
r6a0Xt+xijinut3U7ZzyuM6f1Wm9Juc0pG/n8aBsWm+Im6w/L8sRSr/v3xCpE2tOZSXnDpDF6aZN
bueUB8EQ59QkTrlyhzinUhjzQ//Zz0bTieVAJGdKdAXmBiDF4cqKeYZfilOT0DEdX5fbNGCaxKlr
gJN/447jggvs69l8DeLWW7P3vemOiq/X1ZBtwo/h66lzQySTODW5RWWc09i03ljn9P77sx3pXB2p
Pr8pIyEUFtBcv+SGG/I+hlJFWq8UerzmlAW5S5za7iEH1CmcU1Nbq3LNqW32l/tR2ySc6R2CLuSk
XSiyXpZdc2pqy0R259SX1uu6Dj0pWmTNqbwWndZLFJ7WK5ezFEnr3bYtW08Z0r/5nFMtTtk55XGS
d+st65xKcSrLzefRGyLx9+XxY8SpdE5N98m3W+/8fPauZdkuTeKB8Tmnoe85rXJDJJ8Q0fV5795R
cWr7/txc9qzkTslE5o1tTGm9sh8yibEyE802TM6pT5zaXiVjihdTiFM9AWbCtyGSPoY+XohLyM/N
tvO1vhYfOvY0Oae6flThnKZO641tsxyLhTinqfqDVorT97+f6CMfyf69vJwN0PyA9t/f3NGb0npN
AZepo9FBhEmc8u6nErnrnnzoslHwQ9POqWlWS5aJ04Ue+1jzbBdXbFPnaDq+LrfepEG6anx+eTyN
7tR4kD3uuPydivrafA1Rpp/poMB3TfzcbCKEg4c615zqWVbbrL4rhduHqTMcDMy79RYRp7qcJv77
fx9NNykjTnUZ5cx8kVm/qp3TmLRe+VNSVpxyP+TaEImvP9VuvfIZm56HnliQyGA8tA7KycoQBoPR
vpPb7eKi3VUKWXOqf7qcU9OGSLt3+x0GV1qvFKeuOm0Tp2vWxO3Wy2nERPFpvbxB4WGHlRenOo3Q
5Zz62rvJOdXi1OTsc/uTEysmcepzTvVyINkeijqnUpyuW2dOu2Rc4rTfH0/rbco59Ykm7ZzKtF7b
97dvzzae0kLNFC/6nNMPfjD7T5e7DnHq6qdsab2mCf4Qh1qej+/r3NzofTnyyHzNtw2bcyonVf7u
7/LXPOl6GuIS8nNzOacxab3cDrgcHOfYBLTvfhYRp8NhurTeMs6pHItMxzVlm5ShleJ0166ssyEa
DXKWljKhKjsWKRCJRp1TkziVN87mnOrdeonC15wOBuPi1OScmlIidDnn5zOhZ3KmuFKaxKnvFQ0c
ROt7IdeccsN2DXAm59Tk9mqRZoOfmck55WtzXZNrxlx28PL/Y/E5tLpM8qcrrTflmlN+lkTj68pY
PIWm9epzmWAHQ3+uSNAiJ0l0XdYiNYQqndOlpbi0XvlTHy8krdflnHK9MrU1OYCm2hBJCgmbGN+w
wS5OYweykAkqyfJy1nfqtsfvQ4x1Tvm8enA3HcfmnN5xR/a+7FhxKttTqHPKG8BxGTnQW7s2bs2p
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
25e9u9mX1isnMXQ95xhOX4dM6/Ut25GpxUjrVWjnVK85lTdXBq3cWZp2mTM5gTpws4lTW0U27d5q
E6faOSWyi1Ofc6qDJiZmzamcVZUVi4/pS+vVHbfeOEifzzdTFbLm1Nbpz8/bnVMtTrVzyu8X02WT
QvG66/JNjGzO6cxMdg98ab0251QGH9y57N2bf84kTjnI0vdFCkoepELXnMrz8zVwoKNTHWdn83tr
EtsmAcQiTp+H/y4HX1lvQsQpr7/Sr5LxOSl8vFBxyhNWRKPpZFxeW5sx1WF9XXwd69fnO+zJYxDZ
03o50OV7JtPZZSC6caNbnLr6D11XOYjhPkUGqUXTegcDd1pviDjV1819HJFZBMgAl7MH5LPiQV2K
09A1py5xqt9ZSxS+IZJtwkWLU75mHj99ab0XXUR04om5OCEqt+aUv3/QQUQ33WT/vC+tV2azaOdU
pvWayrW4SLRtW3a9Jud0//3Na06JsvPLMsh2YhKnssyutN6Q3XrZJfY5p3zd7Jy62pdpwmowGD+W
yzmVdcOUqsn9T5kNkeQ6fEa2Ew7WZdym3TwtZGRar8s55bjP55zqeNK1/Eiyb1+2rwDHWrt2Zb83
3S95r3lCzNbu5Hjic075WmxiQ4pT/sn3j1O/bQJSwvEI0WhdkWMJO6ebNo32A6Zj25xTbkf6PKZr
cwk0RrYTuQGeHNc4zj/wwGxM4nZnc07l89HtcHY2ez2Wb0MknrCSAlf2ZTZxyqnPrn57eXm03bpe
JbNtG9Hznpf927Zh0lSKU755pjWnNueUOxOTc7pvXzY4FnVOY9N6eXtrnvXiIMYlTvWGTvI8jEl8
MbFrTuX1y4CJOyVXWq8tjYbIvub0pJOIfvpTc5m0c7pxY9ia0927iZ70JLM45ZlCdpqIRkXA8jLR
s5+dlcklTvfty0Sna0OknTuJHvvYbPZM3hPTmlNTA5ZpZRwcy9QPfq+YDtz4GV19NdHHP56fl58n
B8lyzelznpMNjFq08RojmdrLndLatUT/+I9EH/xg/rd9+/I6LI9jE6d60kgLDC1a5P0LEafz81kb
L7Ih0mBQ3DmVab2csmNqp6b2ZBOnLufUtSESl23PHqKnPMUsTss4p7qu8jlNzmnqDZFixKlrt17T
BIIUp3xsk3MqJ1hczqkUfvoelEnr5d/HOKfPfW7epjZv9ovTq68meve7s6wIPp8Up7FrTvn7i4tu
caoFDv9Op/Xu25dN1DEsylzO6fHHZ/3zVVfl4pTvz+LieJ0OEadr1uTOpd5FnZ3TEHEq+1iTGHOl
9fKEHFEeZ/DY7GpfXA6iPLDna+Frczmn0s2zrSO0Oae33070/OeP/16X0TTmy3ZiE6fSzdOTr660
XpNzKt1Y/r3NOfVNoks4HuVj6HfuSljEEeV9TohzahKnpjWn+vf8N/6Py0CU3z+Z1hvqnBKNi1Nu
d/zvTZvszqlvzSn30Xwe2z2KXXNqck75nvEkBafWc7vTzuk3vpGn1fJ4r5df7N2b1Qlp0PD5ifL6
zuvCpQ6SZp5rzanPKHI5p9oZ3bmTaOvW0b/rPmfq1pwSjd5svebU55zKG8rs3ZvPVOlzSLeTKze7
YzIo0chXi5icU25kprReIrM45Zl5OTOs1zVIZLlC15zqCsozWzLw5zLYgkuXOLWtOb322rwya/Sa
Uxk8uDr9nTuznyZxymWX4lSn9e7alS0Ct4nThYWso3noodzRMrkWO3cSPfKR2czXgw+OXrd2b0xp
vXImXzuXRPn79rSo5fv0ox8Rffe7+XdketZgMJrW+4QnZKLe5JwedNBo58Z1Y82a7GXh0hmenc0/
axKn+p5yGfjvPnEq2x6Xw7fmdPPmYhsi9ftZeWJ36+UJMSlYTAMjtyfbmtOYtF7fhkjch91/v9kl
KZvWK+uqDGJCxSmXt860XhnAmlIkTc6pDhD4+xw08ZhjWiOkhR9/lygsrVc7p/KcRG5xKoO7o4/O
do3n87vEqcyeYfh7HKjLsSJGnHJQy+LHRGha7969o+tAOSZwiVPuk3lHTZ3Wu99+eRvW4nTdulyc
cgofn8eX1hvrnBZJ69XiVAbJtsllLgdf/2AwKnTZObUFsj7n1CVOr7iC6OKLx38vsY35sl/g/sUk
Trk+60A5dEMknoTR47UWp/KZuCb0NSxOdT9nmhjVpknI5pAmcaonTfm4pkww7tOlkCTKMy9id+s1
LamQY8nKSu6c+tJ6dcxClLvYst8s65zK9ionI7lNSLdy9epswozbnd4Q6W1vy95l63JO9+7NHFiZ
ksz9c6+Xj3/c5uUxXM7pYBDvnIa8SmZpKb9OuSZV3vepW3NKNNpxyrRe35pTW1qvyTnVlUN3AjJN
rohzKmebQtJ6uTNm0SHPIz8nXRaTc2pK6ZCwOJUDinZOXYJQzp5LZ4IxBeAysDMhg0ntnNpmUYlG
3+mkHU2TOOV7xwPX8nK2plQ3IJ4ZZud0OMzeYWpL633ooUyYPvKR+aZIXHe0e2NK65XBkuxc+HO+
tF5+Nyp/x5bWK+uOSZwefPC4c8ruDdHo/ZbOqatdyePLv7vEKQstDhBMEygakziNWXPKHX8R57Tf
N88uMrbAxeSccoZImbReoqzey0GOHXTfhki+tF5ZV6Vzqie8fGtObefp99On9fI5icwigINtm3Nq
Eqe9ntk5lc+D/186NjHOKQtgU1pviHMqhdSGDflkqmvNKVHuTLJo4u/INaexzilRvumJCR1o8b+1
c7p377hzKtN6TZkS3G+xoNBpvXLcNDmn/Pz0xEGb0nqlOPW1Ly4HX/9gYE/rNQmXm24anaDTEwsr
K/YsFPnsbLAIdIlTDtZl3CYnNvX3Q5xTGcfpY8py8XWZ6mqIU8TxqL4/PueU+xxbu5Pt2DQBqeMj
rncm08MkTjmmiN2t19T3ykkczl4ISevVEw78fdnHu8Ywn3vIyHbC91U6p/I6Vq/Oym5L611ezjdM
0s4pX9fMTHaM9etHx3buq+VO8jw5oNN6Q9ecusYOGQPJ3Xq1+FxezmNj6Zzq2DakPZhorTjlC9LO
qX6VjHzY3HBszqkprVc2Yi1OZdBlc05tGyLJdY4yrdflnHJnKp1TWYnl5/R9Igpfc6p3FeXOI0ac
xjqncrMlEy7nlDt9U1nk5jA6YDM9C3ao+Hicfm1yuv5/9r48zrKqOnfdqntrrurqarrpLoammRGE
iAFREQQnBEVRA0Kc4hCciPpU1GjEIQ5PMBqf70ViUMlzwhj9xRiHBIf34hifDBFtBERQWqSl6aar
q6u7q6vu+2Ple/s76669zz7n3upueFm/X/9u171n2GefPaxvfd9ee3xc6xT3uOuueEKk++7TxexT
U2H9CJ4b5YhlPEsxp2XgFIBnZiaUk5kpOGq85hRmJ92FBY3cxZhTrm+RIkjwmNMYOMU9LcBAudlJ
xN/sFPM12LoFp7BusvXG0q3bd8zPbMHp7KzPnOKa2GcO9cnRUO5r7XbYT29xMfRbjHn/+q8iL35x
sRwi1ZjTFDjNzdb7rW91bqtVV9aL92yZU3Y2y2S93ppTPp9ZTC/xxu7dRQeS38noaD1ZbxXm1DpN
Ilr2iYlicI77BY9NIiLT0+E8OyeyrLcsCGrBKT5T5bZjnCfrtcwpy3o9x3xmJmTC3L27cysZOJ1w
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
fc06CZFwX7azzhI56ij9v/UJvGt45XpQrzmNMadVZL3IFuVF1QBOcV2R8q1kyqIgIvWZUwZ1Ocyp
iMj69Z1lzMnWy42pVwmRcN7sbLxh9vfvHVlvDJzWZU57CU6XWtYbs7L2DPMmvBio99acfve7/jUZ
nLKsiiOBy5b5jnGOrFdEna1eJkTaW9l6RfT83K1kcpwUNsuc2gkS/7fvCJaawDzmtC445XNXrxZ5
97tFLrrInxy963v18ta36ueNNxaVHUsJTmNsGn//b/8Wvu+FrHdPZevNcdR7BU5zZL25a05Fqs11
nuPJ9ZzK1hurz6pOPu43ONgJdu3f9tp2n9NumVMeHzzmNDUe1ZmHmTkdHvbb91KCU1y/qtUFpzFZ
L4O7HHmyZRvLAl0WwHrgtFvmdHa2+jV4LpiaEvnhD/PP5XbR17d0st6crWRsX4mB05xsvXytbsDp
ZZcVj+H16d417H3QLlP2gGVOm8085rQMnG7aFP+NwSln600lREo14G6YU0ykds2pZdbKLEe+ZZnT
Xm0lg2unZL19fUsr602tOWWZA8pXx0lC1M0zC07LJiBE13mC6LWsN2a5Uj/PsYmBnxjDaI2dQCs/
QftsNP5T1ssG5tReJ8acVmlDljm10iJcP+ZEe+MGzAOnLKuqYt577lbWy7+x87UnZb343msjDxRZ
Lxiy/59lvZY5TW0lY+dY/sw1XMe7XupvkSKQbjZ7C04tc1om603NqTFj5tQjH0Ty2lmdtshb0VW1
qoE5luF6v9XN1ltF1sv9na/fq61k6q45rTuG8DsHc7qvyXpzmFM+384rOe06x1/jgG3sGl65HtDM
aWogTDGnSwFO4ZSUMaepDtSNHAyDq10H22xWi+rkyLdymFM7ueR23DLmFDKOlNVlTlPlZOaUn/8z
nxE59tjye9n79pI5jW0ls9SWK/XzJgEbQeXv+TNmPGjb+uRInMecNps6UOcwpyzr5TJZcHrddUvP
nNadwLnMSyXrTTGn3DbLmNNccMqyqirmsRyeYxtjclP1YreSWUrmNMbyxBhVy5zmbnuyJxMigTnN
aXd7gjnFM+9JWa9lmVJrTtm6YU75H5fN/u2BU2ZO2+3usvVy3VmHOyZvhvWCOY2V98HAnMaCS+gD
Vdac4j1A1uupnew9lpI57YWst6rtKea0LFhgx2WuX+5Te5o5tcekwGld5nSfBacvfanIi14U//2c
c0ROPLHze3aQnvhE/xi2pz1NZMMG/7fJSZE//mP9f6OhLyC15nRkRORlL4vfC42wTgTmjDNEfvtb
XZ+Hvw8+OK/xsB10kMj556ePeehD1YmA9ZI5HRwUuf/+eMN8/vNFVq1KX+Poo0XOPbf8XmedJXLc
ceHvJz5R5CEP8Y896SRdwzUyInLJJeH7448vv4+1detEnvnMzu/f8Q6RE07Q/59wgsjjHifye7+X
vlazqUmUUL9Pf7q++40bq5erqp16ajmLLeI7bEcdpX3UO5Y/Y8bM6fi4yMUXh99GR0M/O/fczndk
wY6IyGGHiZx3Xud9zj7b7899faHNP/nJIj/+sf889rmqgtPTT9ctcaanRS64IH79HOvrW7qESJY5
nZwUecpTtI2MjqrsedUqkd//fW3Xtp/lgNMjjxR5whNEHvUodahe8Yr88sFOPLEzCd7jHidy6KHF
7/r6RP7kT3xwGquXAw7Qd7TUst7HPMbvdy98oZ/g71GP8sFpzrh87LEiT32qvsPY2FhmJ50U5iVY
DITk7O0sou/ssMPqlQd23nk6Vt57r/97o6FjfZVMqi95ST6YPeccbdNsK1eKPO95+n84vd5c+KhH
qUMOq8ucYuy0LMlJJxXX4Fm1lIjIk54U5s8DDgjXS9n55+s8aq2MORVJj0eYN6sYrnvggTr3e/bU
p4a1czFbuVL9kip29NEij3+8yCMeUe08kergdGQkPlY+4Qk6v33+82FMyJX1Pvzh6gc2GjpWxs57
xjNCWzr9dJ3LYN0yp6eeqvPK+vXV/eaHPETn7jo2NaXjrUgInuyNrWROOin0PRF9J/vvH8qFeRyk
mW0zJ54YllEcckjRL1271k+EyZaDL5rNNNB8zGM6x8ynPlV92C99KXHzdru9T/3TItW3j3603T7y
yK4u4dp++7Xby5e32w97WLt9yCHqtr7kJdWu8fGP63l33dW7cj3ykXrNG27o3TWt3Xpru71uXbs9
NtZuX3ON3m9hIfx+7rnt9sqVedd66EPb7Uaj3b7xxqUp64PNTj+93T70UG3X+6rddVe7vWpV3rH/
/u/aft7//vRx73mP9rk6hnucd17e8evX6/F33x2+m59vt/v72+0TTmi3r7++/Bqve51eY36++P2F
F7bbAwPt9lVX5Ze/rg0NtdunnNJuX3tt8fvNm7Vsn/lM+G7Vqmrj0LXXan3UtTvu0DLs2uX/bsu3
t+yqq9rt5z43fczsrJb37/5uz5SprjWb7fZ3vrN37n3PPVpHn/tc+O6739XvHve4vVOmfc0+8Yl2
+6ij2u2TTy4/dtu2amOate99r93+6lfjv7/xje32OefEf9+5U+//mtfUu//jH99uT05qexRpt7//
/fDbc56j333xi/WuHbO77tLrvuAFvb3uUtvtt3f6WN3YTTep77p6dbt96qn6LlJ2yy16/w0bur83
xoFuxsrrrlP/c2Ki+/LUsQsuUJ/1k5/s/bVf8Qr1MerY3/99u33YYTofDQ2122ed1W5/5Su9Ld+G
Dfr+zjgjfswjH9lur11b/dof+1i7/R94z8WC+yxzWteqrqXKtRzmtMy6YU5jVlfuU8Usc2oj8pCL
5NjUlF4nR5b7n6b1vWPH0rE0vbBVq0Te9ra8Y+swp1UN/cxbk546PrbmNKdtp5jTsmQfvbIqa07f
9rZyhQLb6Gh3z1DGBvzf9u4+1paqvOP47zl3nyOv8uoFei8gKheo0QLhzUqRoIDaBpA2RmJbrNWG
VIMpTeNbo/ynJvbFxNb4XjS2Cr5ENG0FA9dEoimttigikljkShRjQNqqsQKrf+w9vfvO3S9r9sya
tZ49309yc8/ZZ58968xeM3s98zxrzazMTQ7nn7/vlf9ZUs857UoXpeKrmpc5leaXWA7NorLeWc+d
/r+p5zxn+esvOr63tqRPfWr17Pr0/Ljq++mf1R/rQtOqslJU0xm6anf1GXTAAXHj4y7fj7a3kqna
sUpZb1eqkvZUZb2r7uf6nNN589fb6KKsd9lrz7N2wWmqQc7GRvvgNMVcpelJ26lMlzjOmlPSpKy3
ChiW1ZtjbHNz+TL7uW1uLi5nn9ZkzumqfbraV7PmpC96/rw5pzFByKI5p9P/pzRv4YbpRU0qse9X
pYvgdNmc7z720TK7du1filnXxzm3C22OobZm7aPqa4LTsUWr9dalDrRiBslXXrn669fLemddtOj6
+J91Uc6DLhYDmzYd3DW5z2kXfa1tWW/1u7mDUylPWe8i9TmnsxZEais2OF1lPL/s7y7847W51JnT
6gqFtHrmtMuDrI+rg/XM6ayVGWO3XwUMBKdxtrbKz5w20WfmNDY4TZ05nf4/JbP4OadNtV0hetmA
K2eWr6lZ9xwtEZnTslVzTmPeo9SBVuqLQ/UFkcicztd1cDoa7Q3umsw57eL9qBZq8p45lcrOnD7x
RL7M6WiUJnPq7LBdLtVJtp45XeWKR4qy3j6u4i8LTpuW9UqU9cbyUNbbxLKV/yptTtpdlfVK/oLT
2NV6mzr00NU+gCpbW8tX9Cshcxpr3oq6JSktOCVzuq8+y3pjXj/l8bcoc9plMDTNa+Z02bmyqdFo
7+dYk8xpF/vNbN+7Xqxi27bxuDvX+bZ6L3LcSmaRKjit3tfY23Q13YbU7lYyy157njUZ8u6V6gN5
Ojh97LHVDrh1yZzW/+4mWS7KepvZ3BwHHN4+YOfpI3O6alnvrH08KxM57zVmPa8aiPdV1psqc7p9
u3T77av//qGHSl/5yvyflzLnNJaXzGmuNpI5Xa6kzGnqCxnV8T3r70hV1us1c3rYYdIdd3T3etP7
ocmc0672WzXXdVXrnDltU9Y7Peao5hXnmnNKWW+EVFfgp8t6H398/GasOufU84JIs0pOVsmcEpzG
SX1Pxb7NyzDOel7fCyLVtzevTHaWee09+eR9t5FSkwWRVtH0fr9Nft9b5nRrq/xjstTMaXXP3KGr
Mqex71HKiw3rWNabOtucUttz7bTpir2+M6dSN5nTEoLT0jKn0+eDbdvSZk5ZEKkDqcpTNjbGAVWV
OT3kkDIyp32V9T7xxPhfF3NOPWQdSlEd9J6ySot4mXMqNQtO52VOTztt322kNG9BJA/lbR4zp5T1
Lt729P/TX5M5HWtS1iulPUZylvWmDk49nVdSmB4j9j3nVBof720zp489lj84LXXOafV1yszpos+6
qmx81dee+7rNX7JsqU7g1SIY1ZzTVTKnKW8lk/LA3djodrVesqbx1i1z2mTOaduy3tjM6bzBUdPM
6aLgtI8B0rz2Vt+XPEjzljn1cIGtzQWetqpbYVDWO1+T1XqltJnTvsp6F2VOKetNYzrAiMmcpijr
bZs5lfLPOS2xrLeUzOkq783ggtOUmdPp1XrbBKceM6eLynqbdM4jjyQ4baIKTksOLJroc87pEUfE
Pb+Lst557X3KU8b/P/xwXFvamLcgkpfgtOT21VHWu1z9mCBzuq+q0iH2PfKcOa1n7cic9qeeOc1R
1ts2cyrlz5yWVtY7KzjNURq/bdvefdTE4ILT44+Xnv3s7l/XbBxU/eIX4yBta6uM4LSPA3c6ON2+
XTr33H1/3uSK7vHHSxdc0H0b19W6ZU5jg9M2J+3q4kfsIHhzU7rkkv0f7yJzaibt3Ck99alxbWmj
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
KmZfP51JQQwAAAAASUVORK5CYII=
"
>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[10]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython2"><pre><span class="n">df</span><span class="p">[</span><span class="s">&#39;sentiment&#39;</span><span class="p">]</span><span class="o">.</span><span class="n">plot</span><span class="o">.</span><span class="n">kde</span><span class="p">(</span><span class="n">figsize</span><span class="o">=</span><span class="p">(</span><span class="mi">16</span><span class="p">,</span> <span class="mi">8</span><span class="p">))</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt output_prompt">Out[10]:</div>


<div class="output_text output_subarea output_execute_result">
<pre>&lt;matplotlib.axes._subplots.AxesSubplot at 0x111094c90&gt;</pre>
</div>

</div>

<div class="output_area"><div class="prompt"></div>


<div class="output_png output_subarea ">
<img src="data:image/png;base64,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
nrZHHdV1NQD00ujoaEZHR3tyrVJb7O0ppRydZHGt9fljn/9lklpr/fvNfM11SZ5ea71no/trm7UC
MLg++tHkkkuST3+660rowo03Jk99anLLLcm8eV1XA0BbSimptU5qmmrbrcgXJjmklHJAKWXbJKck
OWvDE0ope25w+8g0YfueAMAYbcgz26JFyTOekXz5y11XAsCgajXY1lrXJHljku8kuSzJF2utV5RS
Ti2lvG7stBeXUn5eSrkkyQeTvKTNmgAYLmvWJKOjyXOe03UldOmP/ij52Me6rgKAQdVqK3IvaUUG
mJnOO68JNT/9adeV0KWHH04e85jkG99IDj+862oAaMMgtyIDwJScfXZy4oldV0HX5sxJXve65OMf
77oSAAaREVsABtrhhzctqMce23UldO2225InPjG54YZkhx26rgaAXjNiC8C0dNNNzUq4Rx/ddSUM
gr33Tp773OSMM7quBIBBI9gCMLC++c3k+OOT2bO7roRB8Sd/knzoQ82iYgCwjmALwMD62teSF72o
6yoYJM9+drLbbslXv9p1JQAMEnNsARhId9+dHHRQ04q8YEHX1TBIzjwz+Z//M/nJT5IyqZlYAAwi
c2wBmHa++tXkec8Tanm0k05KVqxIvv/9risBYFAItgAMpC9+MTnllK6rYBDNmpW87W3J3/9915UA
MCi0IgMwcO64I3n845vtXebP77oaBtGqVcnBBydf+Upy5JFdVwNAL2hFBmBa+cIXmnZToZZNmTs3
ede7kne8o+tKABgEgi0AA6XW5BOfSF73uq4rYdC99rXJDTck3/te15UA0DXBFoCB8oMfNPvWHnts
15Uw6LbZJnnve5O3v92+tgAznWALwED5xCeSU0+1jQsT83u/l8ybl3z6011XAkCXLB4FwMC4+ebk
KU9JfvnLZOedu66GYbFkSXL88cnllye77tp1NQBM1lQWjxJsARgYf/qnTRvyP/5j15UwbP7kT5q9
bf/1X7uuBIDJEmwBGHp33pkcemjy858n++zTdTUMm/vuSw4/PPnAB5KTT+66GgAmw3Y/AAy9D3wg
eclLhFomZ8GC5LOfTV7/+uT227uuBoB+M2ILQOeuuy55xjOauZL77991NQyzxYuTc89NzjmnWTUZ
gOGhFRmAofbiFzdtpO96V9eVMOzWrm1akQ84IPnIR6yuDTBMtCIDMLS++93koouSt76160qYDmbN
Sj73uWY/5L/7u66rAaBf5nRdAAAz1z33JK99bbMH6fz5XVfDdLHTTsm3v508+9nJ9tsnb3pT1xUB
0DatyAB0otbkpS9N9tgj+fCHu66G6ei665LnPjd51auSd75TWzLAoDPHFoCh87/+V/L5zyc//rHR
Wtpz++3JCSckT35ycvrpyXbbdV0RAJtiji0AQ+XMM5MPfjD5+teFWtq1117Jeec1t48+Orn66m7r
AaAdgi0AfXXWWcnrXteEW1v70A/bbdfscfuGNyTHHNPsmbxmTddVAdBLWpEB6JvPfz758z9Pzj67
2bcW+u2aa5o/rKxY0WwHdPTRXVcEwDrm2AIw0B56KHnHO5KvfjX52teSJz2p64qYyWpNzjijWVDq
qKOSv/mb5HGP67oqAMyxBWBgXXxx8sxnJlddlVx4oVBL90ppVkr+xS+azoFjj01+7/ea/ZQBGE6C
LQCt+NWvmrbj5z8/eetbm7m1u+zSdVWw3vz5yV/+ZbMt0DHHJL/9201r8qc+lSxf3nV1AGwNwRaA
nlqxInnPe5JDD00eeCD52c+SV7zCHqIMrgULkj/7sybgvutdybe+ley7b7MH7j/9U3LBBcnKlV1X
CcDmmGMLQE88+GCzT+jf/V3yW7+V/PVfJwcf3HVVMDkrViTnnNOE3AsvTK68Mtlvv+bYZ58m+O65
5yOPQw6xfRXAVFg8CoDOPPRQ8pnPJO97X/L0pyfvfW/ylKd0XRX01kMPNSsq33rr+uP225M77miO
229Prr8+Oeig5Mgjkxe8oGnDX7Cg68oBhodgC0DfrV2bfO5zyeLFzYqy731v8ws9zFSrViWXXZac
f37y9a83I72veEXyR3+UPP7xXVcHMPgEWwD66uKLm1/Wk+T9709+4ze6rQcG0Y03Nu35//zPyQkn
NH/8WbSo66oABpftfgDoi3vvTf74j5s2y9e9rhmZEmphfIsWNXvkXnNNc/upT21WYV6xouvKAKYf
wRaALVq7NvnXf02e+MTm9uWXJ699bTLLTxHYoh12aEZrL700ue225AlPSL7whUQjGkDvaEUGYLN+
+tNmlPahh5KPfSx5xjO6rgiG23nnJW98Y7JwYfKRjySHH951RQCDQSsyAD13zz3Jn/xJ8rznJa96
VfJ//69QC71w7LHJf/1X8vu/37y/3vjGps0fgMkTbAF4hIcfTk47LTn00PVtx3/4h9qOoZdmz05e
//rm/bVmTdOe/KlPNbcB2HpakQFI0vxC/aUvNXMB99wz+dCHkic/ueuqYGa45JJm5HbVquSDH2xG
dcukmvEAhpftfgCYtKVLk//9v5sgu+uuybvelRx/vF+qod9qTT7/+WZv6F12aaYC/M7vJNtv33Vl
AP0x0MG2lPL8JB9M0/b86Vrr349zzoeTnJDk/iSvrrUuGeccwXaIjY6OZmRkpOsymASv3XDb1Ot3
773Jd76TnHVWcvbZTZB9/euTkRGBdpB4/w2vqbx2a9Yk3/pWMyXgvPOS//bfkhe9qBnFfdzjpvYe
ffjh5M47m9WZNz7uvDN54IHmePDB5uOqVc3XzZrVPO+Gx6xZyTbbJHPnJvPmPfrYaacmoO+6a/Nx
l12SvfdO9t23WSl60KxZk9x/f/PvvuCC0TzveSOZO9f3xGHj++Zwm0qwndPrYjZUSpmV5KNJ/luS
W5NcWEr5Wq31yg3OOSHJwbXWx5ZSjkpyepKj26yL/vNNZngNw2tXa/PL2urV439cs2b9L18bHjNh
zug554xm0aKRXHtts5fmxRc3i9Zcc02z/+yJJzYjtbvt1nWljGcY3n+Mbyqv3ezZyQtf2Bz33JN8
4xtN0H3Pe5o9cJ/whOSgg5q9cXfcsQmJCxY0c+Ifeqg5li9vgupddzUf77ijCa93390Ezb33fuTx
pCcle+yRbLddMn9+c8yb13yvTJrvs2vXNh/XHWvXNt9jH3ywCcAPPrj+eOCBZNmy5vmuu675d/zq
V00Nt9zShMV9922O/fZbf3uffdYfe+3VfO/uhQceSG66KbnhhkcfN97Y1PXQQ+v//StWjKbWkaxe
ney88/ra9t03OfDA5IADmo8HHtjcP6fV36jZGr5vzlxtvw2PTHJ1rfWGJCmlfDHJyUmu3OCck5Oc
kSS11gtKKTuWUvastd7Rcm1AS2ptfsl54IFk5crkvvuav4Lff//62+Pdt7nbq1dvPrjOnt38AjRn
zqM/zprVnLtq1frjoYeSbbdtRhR23vmRHze8veOOzbHu9oYf58/vz1/ya23+Oy5fPv6x7pfHu+5q
fnHc8ONddyVnnJEcfHDzi/BTn5r8wR8024vMm9d+7cDU7LJL8spXNkeS3H57ctVVyS9/2QS1229P
rr66CbyzZzff17bdttlKaK+9kqc8pQmse+zRBNg99ug+hNXafO+6+eYm5K47fv7zppPk1lub4847
m+/F64Lurrs+8nvyuu9h60aQH354/ffFpUuba6x7jhUrkv33bwLpokXNx+c8Z/3tvfduQu267+mL
FzfHmjVNKF9X07pw/J3vJNdf3xx33dXUt2Hg3fDj7rs37eQz4Y+p0KW2v7Xtm+SmDT6/OU3Y3dw5
t4zdN3TB9qtfTT796fEf21wX9aYem8zXtPFYL6533XXJD3/Yn+fqxWPT9bkmU8dttyVf+9qmr7d2
7frWtXVB9sEHm1A5f37zi8KCBc0P9e23X3974/v23nv8+9fd3nbb5pex8YLrnDlbHzBrbepctqxp
y126tDnW3b733iYcXnNNc87SpY/8uGxZE5YXLGhqmzt3/S+UG97eUl3rRpvXhe2HHlp/e93HBx9s
rrXDDuuPdaM0645dd00OO6wZed1tt+YXqd12Sz7+8WYxKGB62Guv5jjuuK4rmbxS1gfUww7b9Hlr
1jSh8dZbm3C67vvzsmXNCPSqVY8cQZ4zp/l+uPvuzR/zTjqpGQ3eb7/m++Fk/hA5e3Zzvd133/R+
ww891ATe669vQu/11yejo+uD7913Nz8ft9uu+YPDwoVNKJ89e/3PsI1vb67WLf07Jvu106Xl+qqr
kosu6roKfvu3mz+k91Orc2xLKb+T5Pha6+vGPn95kiNrrW/a4JyvJ/nbWuv5Y59/L8lf1Fov3uha
JtgCAABMYwM5xzbN6OuiDT7fb+y+jc/ZfwvnTPofCAAAwPTWdrf/hUkOKaUcUErZNskpSc7a6Jyz
krwySUopRydZan4tAAAAE9XqiG2tdU0p5Y1JvpP12/1cUUo5tXm4frLW+s1SygtKKdek2e7nNW3W
BAAAwPTS+j62AAAA0KaBXXi8lPL+UsoVpZQlpZT/KKWMu5V3KeX5pZQrSym/KKW8vd91Mr5SyotL
KT8vpawppTxtM+ddX0r5aSnlklLKT/pZI+PbitfOe28AlVJ2LqV8p5RyVSnl26WUHTdxnvfegJjI
e6mU8uFSytVjPxOP6HeNbNqWXr9SynGllKWllIvHjnd2USePVkr5dCnljlLKzzZzjvfegNrS6+e9
N7hKKfuVUs4tpVxWSrm0lPKmTZy3Ve+/gQ22adqXD6u1HpHk6iT/Y+MTSimzknw0yfFJDkvy0lLK
oX2tkk25NMn/m+QHWzhvbZKRWutTa60bbwVFN7b42nnvDbS/TPK9Wuvjk5ybcb53jvHeGwATeS+V
Uk5IcnCt9bFJTk1yet8LZVxb8b3wh7XWp40d7+trkWzOv6R57cblvTfwNvv6jfHeG0wPJ3lLrfWw
JMck+eNe/Owb2GBba/1erXXt2Kf/N81qyRs7MsnVtdYbaq2rk3wxycn9qpFNq7VeVWu9OsmWVrMu
GeD/D2eiCb523nuD6+Qknx27/dkkv72J87z3BsNE3ksnJzkjSWqtFyTZsZSyZ3/LZBMm+r3Qzg4D
qNb6oyT3buYU770BNoHXL/HeG0i11ttrrUvGbt+X5Iok+2502la//4bll5rXJvnWOPfvm+SmDT6/
OY/+j8Jgq0m+W0q5sJTyh10Xw4R57w2uPdatLF9rvT3JHps4z3tvMEzkvbTxObeMcw7dmOj3wmPG
WunOLqU8sT+l0QPee8PPe2/AlVIOTHJEkgs2emir339t72O7WaWU7ybZMHmXNL9s/VWt9etj5/xV
ktW11i90UCKbMZHXbwKOrbXeVkrZPc0v2VeM/QWOFvXotaMjm3n9xps/tKkVAr33oD8uSrKo1rpy
rLXuzCSP67gmmAm89wZcKWVBki8nefPYyO2UdBpsa63P3dzjpZRXJ3lBkt/cxCm3JFm0wef7jd1H
H2zp9ZvgNW4b+3hXKeX/b+9+XmUK4ziOvz/SXbBDYaG78TdI2VgJSRZCKb82IlsbG2tLKQtiIxY2
NzdR/gJlQREbG8qChWwkSV+LMzdT7jFz/ZhzTr1fq6nzND31nU/n+c48z5kFmm1dLq7/s39QO7PX
od/Vb/QgjY1V9T7JJuBDy3uYvX6YJkvvgC0TxqgbE+s3vlirqodJriZZV1UfZzRH/TmzN2Bmr9+S
rKZpam9V1b1lhqw4f73dipxkN3Ae2F9VX1uGPQG2JplPMgccARZnNUdNbdnzDUnWjL6pIclaYBfw
YpYT00RtZ1PMXn8tAidGr48Dv9wszF6vTJOlReAYQJLtwKel7ebq3MT6jZ8JS7KN5q8WXVj3R2i/
15m9/mutn9nrvZvAy6q63HJ9xfnr9BfbCa4AczRb5AAeV9XZJJuB61W1r6q+JzlH8wTlVcCNqnrV
3ZS1JMkBmhpuAO4neVZVe8brR7OVciFJ0XwWb1fVo+5mLZiudmav1y4Bd5OcAt4AhwDMXj+1ZSnJ
6eZyXauqB0n2JnkNfAZOdjln/TRN/YCDSc4A34AvwOHuZqxxSe4AO4H1Sd4CF2nWnmZvACbVD7PX
W0l2AEeB50me0hybugDM8xf5S1Xb8StJkiRJkvqvt1uRJUmSJEmaho2tJEmSJGnQbGwlSZIkSYNm
YytJkiRJGjQbW0mSJEnSoNnYSpIkSZIGzcZWkiRJkjRoPwDDKtEZhDNudwAAAABJRU5ErkJggg==
"
>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h3 id="Mining-text">Mining text<a class="anchor-link" href="#Mining-text">&#182;</a></h3><p>The regular expresions library will be used to mine text</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[12]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython2"><pre><span class="kn">import</span> <span class="nn">re</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>And a function created to separate the different terms tracked</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[13]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython2"><pre><span class="k">def</span> <span class="nf">wordInText</span><span class="p">(</span><span class="n">word</span><span class="p">,</span> <span class="n">text</span><span class="p">):</span>
    <span class="n">word</span> <span class="o">=</span> <span class="n">word</span><span class="o">.</span><span class="n">lower</span><span class="p">()</span>
    <span class="n">text</span> <span class="o">=</span> <span class="n">text</span><span class="o">.</span><span class="n">lower</span><span class="p">()</span>
    <span class="n">match</span> <span class="o">=</span> <span class="n">re</span><span class="o">.</span><span class="n">search</span><span class="p">(</span><span class="n">word</span><span class="p">,</span> <span class="n">text</span><span class="p">)</span>
    <span class="k">if</span> <span class="n">match</span><span class="p">:</span>
        <span class="k">return</span> <span class="mi">1</span>
    <span class="k">return</span> <span class="mi">0</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>Create new columns corresponding to term in tweet.</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[14]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython2"><pre><span class="c"># New column equals applying the wordInText function to every element of the column text</span>
<span class="n">df</span><span class="p">[</span><span class="s">&#39;red&#39;</span><span class="p">]</span> <span class="o">=</span> <span class="n">df</span><span class="p">[</span><span class="s">&#39;tweet&#39;</span><span class="p">]</span><span class="o">.</span><span class="n">apply</span><span class="p">(</span><span class="k">lambda</span> <span class="n">tweet</span><span class="p">:</span> <span class="n">wordInText</span><span class="p">(</span><span class="s">&#39;red&#39;</span><span class="p">,</span> <span class="n">tweet</span><span class="p">))</span>
<span class="n">df</span><span class="p">[</span><span class="s">&#39;green&#39;</span><span class="p">]</span> <span class="o">=</span> <span class="n">df</span><span class="p">[</span><span class="s">&#39;tweet&#39;</span><span class="p">]</span><span class="o">.</span><span class="n">apply</span><span class="p">(</span><span class="k">lambda</span> <span class="n">tweet</span><span class="p">:</span> <span class="n">wordInText</span><span class="p">(</span><span class="s">&#39;green&#39;</span><span class="p">,</span> <span class="n">tweet</span><span class="p">))</span>
<span class="n">df</span><span class="p">[</span><span class="s">&#39;blue&#39;</span><span class="p">]</span> <span class="o">=</span> <span class="n">df</span><span class="p">[</span><span class="s">&#39;tweet&#39;</span><span class="p">]</span><span class="o">.</span><span class="n">apply</span><span class="p">(</span><span class="k">lambda</span> <span class="n">tweet</span><span class="p">:</span> <span class="n">wordInText</span><span class="p">(</span><span class="s">&#39;blue&#39;</span><span class="p">,</span> <span class="n">tweet</span><span class="p">))</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[15]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython2"><pre><span class="n">df</span><span class="o">.</span><span class="n">head</span><span class="p">()</span> <span class="c"># How the data looks like</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt output_prompt">Out[15]:</div>

<div class="output_html rendered_html output_subarea output_execute_result">
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>tweet</th>
      <th>sentiment</th>
      <th>red</th>
      <th>green</th>
      <th>blue</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>RT @5REDVELVET: [OFFICIAL] 160315 RED VELVET #...</td>
      <td>-0.375000</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>RT @WampsBraintree: Wamp Train scheduled for 5...</td>
      <td>0.000000</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>RT @thickred3x: Order Red &amp;amp; @JovanJordanXX...</td>
      <td>0.000000</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>@lipdistrikt Thks 4 following! - Please vote f...</td>
      <td>0.166667</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>RT @UFCONFOX: Dustin Poirier vs. Bobby Green j...</td>
      <td>-0.200000</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[16]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython2"><pre><span class="k">print</span> <span class="n">df</span><span class="p">[</span><span class="s">&#39;red&#39;</span><span class="p">]</span><span class="o">.</span><span class="n">value_counts</span><span class="p">()</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt"></div>
<div class="output_subarea output_stream output_stdout output_text">
<pre>0    654
1    461
Name: red, dtype: int64
</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[17]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython2"><pre><span class="n">df</span><span class="p">[[</span><span class="s">&#39;red&#39;</span><span class="p">,</span><span class="s">&#39;green&#39;</span><span class="p">,</span><span class="s">&#39;blue&#39;</span><span class="p">]]</span><span class="o">.</span><span class="n">sum</span><span class="p">()</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt output_prompt">Out[17]:</div>


<div class="output_text output_subarea output_execute_result">
<pre>red      461
green    249
blue     410
dtype: int64</pre>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[18]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython2"><pre><span class="n">df</span><span class="p">[[</span><span class="s">&#39;red&#39;</span><span class="p">,</span><span class="s">&#39;green&#39;</span><span class="p">,</span><span class="s">&#39;blue&#39;</span><span class="p">]]</span><span class="o">.</span><span class="n">sum</span><span class="p">()</span><span class="o">.</span><span class="n">plot</span><span class="p">(</span><span class="n">kind</span><span class="o">=</span><span class="s">&#39;bar&#39;</span><span class="p">,</span><span class="n">color</span><span class="o">=</span><span class="p">[</span><span class="s">&#39;r&#39;</span><span class="p">,</span><span class="s">&#39;g&#39;</span><span class="p">,</span><span class="s">&#39;b&#39;</span><span class="p">],</span><span class="n">figsize</span><span class="o">=</span><span class="p">(</span><span class="mi">16</span><span class="p">,</span> <span class="mi">8</span><span class="p">))</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt output_prompt">Out[18]:</div>


<div class="output_text output_subarea output_execute_result">
<pre>&lt;matplotlib.axes._subplots.AxesSubplot at 0x111840110&gt;</pre>
</div>

</div>

<div class="output_area"><div class="prompt"></div>


<div class="output_png output_subarea ">
<img src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAA6IAAAHyCAYAAADx6XNZAAAABHNCSVQICAgIfAhkiAAAAAlwSFlz
AAALEgAACxIB0t1+/AAAGXNJREFUeJzt3X+MZXd53/HPYwyIHw2y2nq3ssHQGoGdKEBFnASqdhS1
JtDEtqrKJYkqkNuKyFSgJq2wW1VMpaiJUSuUKqL9gxRtUpDrRGoxRMUOPyZpEsVAMISyxrWU2HFW
2U2bRk0paWLD0z/mrjNsdr137TvP8ey8XpK195w5d+6z4527897zvedWdwcAAACmXLL0AAAAABwu
QhQAAIBRQhQAAIBRQhQAAIBRQhQAAIBRQhQAAIBRa4VoVT1cVV+oqvur6tOrfZdV1b1V9WBV3VNV
L9pz/O1V9VBVPVBV1+/X8AAAABw8654R/XqSre5+TXdft9p3W5KPd/crknwyye1JUlXXJrk5yTVJ
3pjkfVVVmx0bAACAg2rdEK2zHHtjkmOr28eS3LS6fUOSO7v78e5+OMlDSa4LAAAAZP0Q7SQ/X1Wf
qaq/v9p3pLtPJUl3n0xy+Wr/FUke3XPfE6t9AAAAkEvXPO713f07VfXnk9xbVQ9mN073OnP7SVXV
BR0PAADAwdLdZ32Z5loh2t2/s/r1f1TVf87uUttTVXWku09V1dEkv7s6/ESSF++5+5WrfWf7vGuO
D+e3vb2d7e3tpccAOCfPU8AzmecoNu3JLhV03qW5VfX8qnrh6vYLklyf5ItJ7k7y1tVhb0ny4dXt
u5O8uaqeU1UvS3J1kk8/1eEBAAC4uKxzRvRIkv+0Wkp7aZIPdve9VfXZJHdV1S1JHsnulXLT3cer
6q4kx5M8luTWduoTAACAlfOGaHf/ZpJXn2X//0ry189xnx9N8qNPezq4AFtbW0uPAPCkPE8Bz2Se
o5hUS52srConSgEAAC5SVXXOixWt+/YtAAAAsBFCFAAAgFFCFAAAgFFCFAAAgFFCFAAAgFFCFAAA
gFFCFAAAgFFCFAAAgFFCFAAAgFFCFAAAgFFCFAAAgFFCFAAAgFFCFAAAgFFCFAAAgFFCFAAAgFFC
FAAAgFFCFAAAgFFCFAAAgFFCFAAAgFFCFAAAgFFCFAAAgFFCFAAAgFFCFAAAgFFCFAAAgFFCFAAA
gFFCFAAAgFFCFAAAgFFCFAAAgFFCFAAAgFGXLj0A5/fSo0fzyKlTS4/BReSqI0fy8MmTS48BAMAh
Vd29zANX9VKPfdBUVXyl2KRK4vsPAID9VFXp7jrbxyzNBQAAYJQQBQAAYJQQBQAAYJQQBQAAYJQQ
BQAAYJQQBQAAYJQQBQAAYJQQBQAAYJQQBQAAYJQQBQAAYJQQBQAAYJQQBQAAYJQQBQAAYJQQBQAA
YJQQBQAAYJQQBQAAYJQQBQAAYJQQBQAAYJQQBQAAYJQQBQAAYJQQBQAAYJQQBQAAYJQQBQAAYJQQ
BQAAYJQQBQAAYJQQBQAAYJQQBQAAYJQQBQAAYJQQBQAAYJQQBQAAYJQQBQAAYJQQBQAAYJQQBQAA
YJQQBQAAYJQQBQAAYJQQBQAAYJQQBQAAYJQQBQAAYJQQBQAAYJQQBQAAYJQQBQAAYJQQBQAAYJQQ
BQAAYJQQBQAAYNSlSw8AAAD76ejRl+bUqUeWHoOLyJEjV+XkyYeXHuNAq+5e5oGreqnHPmiqKr5S
bFIl8f0HwGFRVYmfptio8rPUGqoq3V1n+5iluQAAAIwSogAAAIxaO0Sr6pKq+lxV3b3avqyq7q2q
B6vqnqp60Z5jb6+qh6rqgaq6fj8GBwAA4GC6kDOi70xyfM/2bUk+3t2vSPLJJLcnSVVdm+TmJNck
eWOS99XuwnwAAABYL0Sr6sokb0ry/j27b0xybHX7WJKbVrdvSHJndz/e3Q8neSjJdRuZFgAAgANv
3TOi703yT/KNlxs70t2nkqS7Tya5fLX/iiSP7jnuxGofAAAAnD9Eq+pvJjnV3Z/P7rs+nIvrFwMA
AHBel65xzOuT3FBVb0ryvCR/pqp+OsnJqjrS3aeq6miS310dfyLJi/fc/8rVvj9le3v7idtbW1vZ
2tq64N8AAAAAy9vZ2cnOzs5ax9aFvBFrVf21JD/c3TdU1XuS/F5331FV70pyWXfftrpY0QeTfHt2
l+T+fJKX9xkPVFVn7uIcqsrpZjaqEm/CDMChsXvdTH/vsUnlZ6k1VFW6+6yratc5I3ouP5bkrqq6
Jckj2b1Sbrr7eFXdld0r7D6W5FbFCQAAwGkXdEZ0ow/sjOjanBFl05wRBeAwcUaUzXNGdB1Pdkb0
Qt5HFAAAAJ42IQoAAMAoIQoAAMAoIQoAAMAoIQoAAMAoIQoAAMAoIQoAAMAoIQoAAMAoIQoAAMAo
IQoAAMAoIQoAAMAoIQoAAMAoIQoAAMAoIQoAAMAoIQoAAMAoIQoAAMAoIQoAAMAoIQoAAMAoIQoA
AMAoIQoAAMAoIQoAAMAoIQoAAMAoIQoAAMAoIQoAAMAoIQoAAMAoIQoAAMAoIQoAAMAoIQoAAMAo
IQoAAMAoIQoAAMAoIQoAAMAoIQoAAMAoIQoAAMAoIQoAAMAoIQoAAMAoIQoAAMAoIQoAAMAoIQoA
AMAoIQoAAMAoIQoAAMAoIQoAAMAoIQoAAMAoIQoAAMAoIQoAAMAoIQoAAMAoIQoAAMAoIQoAAMAo
IQoAAMAoIQoAAMAoIQoAAMAoIQoAAMAoIQoAAMAoIQoAAMAoIQoAAMAoIQoAAMAoIQoAAMAoIQoA
AMAoIQoAAMAoIQoAAMAoIQoAAMAoIQoAAMAoIQoAAMAoIQoAAMAoIQoAAMAoIQoAAMAoIQoAAMAo
IQoAAMAoIQoAAMAoIQoAAMAoIQoAAMAoIQoAAMAoIQoAAMAoIQoAAMAoIQoAAMAoIQoAAMAoIQoA
AMAoIQoAAMAoIQoAAMAoIQoAAMAoIQoAAMAoIQoAAMCo84ZoVT23qu6rqvur6ktV9S9X+y+rqnur
6sGquqeqXrTnPrdX1UNV9UBVXb+fvwEAAAAOluru8x9U9fzu/mpVPSvJLyf54SQ3JPm97n5PVb0r
yWXdfVtVXZvkg0m+LcmVST6e5OV9xgNV1Zm7OIeqiq8Um1RJfP8BcFhUVeKnKTaq/Cy1hqpKd9fZ
PrbW0tzu/urq5nNX9/n9JDcmObbafyzJTavbNyS5s7sf7+6HkzyU5LqnNjoAAAAXm7VCtKouqar7
k5xMstPdx5Mc6e5TSdLdJ5Ncvjr8iiSP7rn7idU+AAAAyKXrHNTdX0/ymqr6piT3VNVW/vT6hgs+
N729vf3E7a2trWxtbV3opwAAAOAZYGdnJzs7O2sdu9ZrRL/hDlX/PMkfJvl7Sba6+1RVHU3yqe6+
pqpuS9Ldfcfq+I8leXd333fG5/Ea0TV5jSib5jWiABwmXiPK5nmN6Dqe1mtEq+rPnb4iblU9L8nf
SHJ/kruTvHV12FuSfHh1++4kb66q51TVy5JcneTTT+t3AAAAwEVjnaW5fyHJsdr9p6RLkvx0d39i
9ZrRu6rqliSPJLk5Sbr7eFXdleR4kseS3OrUJwAAAKdd8NLcjT2wpblrszSXTbM0F4DDxNJcNs/S
3HU87bdvAQAAgE0RogAAAIwSogAAAIwSogAAAIwSogAAAIwSogAAAIwSogAAAIwSogAAAIwSogAA
AIwSogAAAIwSogAAAIwSogAAAIwSogAAAIwSogAAAIwSogAAAIwSogAAAIwSogAAAIwSogAAAIwS
ogAAAIwSogAAAIwSogAAAIwSogAAAIwSogAAAIwSogAAAIwSogAAAIwSogAAAIwSogAAAIwSogAA
AIwSogAAAIwSogAAAIwSogAAAIwSogAAAIwSogAAAIwSogAAAIwSogAAAIwSogAAAIwSogAAAIwS
ogAAAIwSogAAAIwSogAAAIy6dOkBADjYjl55NKdOnFp6DC4iR644kpO/fXLpMQDYR9XdyzxwVS/1
2AdNVcVXik2qJL7/2JSqSraXnoKLyrbnKDarqhI/TbFR5XlqDVWV7q6zfczSXAAAAEYJUQAAAEYJ
UQAAAEYJUQAAAEYJUQAAAEYJUQAAAEYJUQAAAEYJUQAAAEYJUQAAAEYJUQAAAEYJUQAAAEYJUQAA
AEYJUQAAAEYJUQAAAEYJUQAAAEYJUQAAAEYJUQAAAEYJUQAAAEYJUQAAAEYJUQAAAEYJUQAAAEYJ
UQAAAEYJUQAAAEYJUQAAAEYJUQAAAEYJUQAAAEYJUQAAAEYJUQAAAEYJUQAAAEYJUQAAAEYJUQAA
AEYJUQAAAEYJUQAAAEYJUQAAAEYJUQAAAEYJUQAAAEYJUQAAAEYJUQAAAEadN0Sr6sqq+mRVfamq
vlhV71jtv6yq7q2qB6vqnqp60Z773F5VD1XVA1V1/X7+BgAAADhY1jkj+niSH+rub07ynUneXlWv
THJbko939yuSfDLJ7UlSVdcmuTnJNUnemOR9VVX7MTwAAAAHz3lDtLtPdvfnV7e/kuSBJFcmuTHJ
sdVhx5LctLp9Q5I7u/vx7n44yUNJrtvw3AAAABxQF/Qa0ap6aZJXJ/nVJEe6+1SyG6tJLl8ddkWS
R/fc7cRqHwAAAOTSdQ+sqhcm+dkk7+zur1RVn3HImdvntb29/cTtra2tbG1tXeinAAAA4BlgZ2cn
Ozs7ax1b3efvx6q6NMlHk/yX7v7x1b4Hkmx196mqOprkU919TVXdlqS7+47VcR9L8u7uvu+Mz9nr
PDZJVV145cOTqCS+/9iUqkq2l56Ci8q25yg2a/dyJf5MsUnleWoNVZXuPuv1gtZdmvvvkxw/HaEr
dyd56+r2W5J8eM/+N1fVc6rqZUmuTvLpC54aAACAi9J5l+ZW1euT/ECSL1bV/dn956R/muSOJHdV
1S1JHsnulXLT3cer6q4kx5M8luRWpz4BAAA4ba2lufvywJbmrs3SXDbN0lw2ydJcNm7bcxSbZWku
m2dp7jo2sTQXAAAANkKIAgAAMEqIAgAAMEqIAgAAMEqIAgAAMEqIAgAAMEqIAgAAMEqIAgAAMEqI
AgAAMEqIAgAAMEqIAgAAMEqIAgAAMEqIAgAAMEqIAgAAMEqIAgAAMEqIAgAAMEqIAgAAMEqIAgAA
MEqIAgAAMEqIAgAAMEqIAgAAMEqIAgAAMEqIAgAAMEqIAgAAMEqIAgAAMEqIAgAAMEqIAgAAMEqI
AgAAMEqIAgAAMEqIAgAAMEqIAgAAMEqIAgAAMEqIAgAAMEqIAgAAMEqIAgAAMEqIAgAAMEqIAgAA
MEqIAgAAMEqIAgAAMEqIAgAAMEqIAgAAMEqIAgAAMEqIAgAAMEqIAgAAMEqIAgAAMEqIAgAAMEqI
AgAAMEqIAgAAMEqIAgAAMEqIAgAAMEqIAgAAMEqIAgAAMEqIAgAAMEqIAgAAMEqIAgAAMEqIAgAA
MEqIAgAAMEqIAgAAMEqIAgAAMEqIAgAAMEqIAgAAMEqIAgAAMEqIAgAAMEqIAgAAMEqIAgAAMEqI
AgAAMEqIAgAAMEqIAgAAMEqIAgAAMEqIAgAAMEqIAgAAMEqIAgAAMEqIAgAAMEqIAgAAMEqIAgAA
MEqIAgAAMEqIAgAAMEqIAgAAMEqIAgAAMEqIAgAAMOq8IVpVP1lVp6rq1/fsu6yq7q2qB6vqnqp6
0Z6P3V5VD1XVA1V1/X4NDgAAwMG0zhnRDyR5wxn7bkvy8e5+RZJPJrk9Sarq2iQ3J7kmyRuTvK+q
anPjAgAAcNCdN0S7+5eS/P4Zu29Mcmx1+1iSm1a3b0hyZ3c/3t0PJ3koyXWbGRUAAICLwVN9jejl
3X0qSbr7ZJLLV/uvSPLonuNOrPYBAABAkuTSDX2efip32t7efuL21tZWtra2NjQOAAAAk3Z2drKz
s7PWsdV9/oasqquSfKS7v3W1/UCSre4+VVVHk3yqu6+pqtuSdHffsTruY0ne3d33neVz9jqPTVJV
T6304Rwqie8/NqWqku2lp+Cisu05is3avWSJP1NsUnmeWkNVpbvPes2gdZfm1uq/0+5O8tbV7bck
+fCe/W+uqudU1cuSXJ3k0xc8MQAAABet8y7NraoPJdlK8mer6reSvDvJjyX5maq6Jckj2b1Sbrr7
eFXdleR4kseS3Oq0JwAAAHuttTR3Xx7Y0ty1WZrLplmayyZZmsvGbXuOYrMszWXzLM1dxyaW5gIA
AMBGCFEAAABGCVEAAABGCVEAAABGCVEAAABGCVEAAABGCVEAAABGCVEAAABGCVEAAABGCVEAAABG
CVEAAABGCVEAAABGCVEAAABGCVEAAABGCVEAAABGCVEAAABGCVEAAABGCVEAAABGCVEAAABGCVEA
AABGCVEAAABGCVEAAABGCVEAAABGCVEAAABGCVEAAABGCVEAAABGCVEAAABGCVEAAABGCVEAAABG
CVEAAABGCVEAAABGCVEAAABGCVEAAABGCVEAAABGCVEAAABGCVEAAABGCVEAAABGCVEAAABGCVEA
AABGCVEAAABGCVEAAABGCVEAAABGCVEAAABGCVEAAABGCVEAAABGCVEAAABGCVEAAABGCVEAAABG
CVEAAABGCVEAAABGCVEAAABGCVEAAABGCVEAAABGCVEAAABGCVEAAABGCVEAAABGCVEAAABGCVEA
AABGCVEAAABGCVEAAABGCVEAAABGCVEAAABGCVEAAABGCVEAAABGCVEAAABGCVEAAABGCVEAAABG
CVEAAABGCVEAAABGCVEAAABGCVEAAABGCVEAAABGCVEAAABGCVEAAABGCVEAAABGCVEAAABGCVEA
AABGCVEAAABGCVEAAABGCVEAAABGCVEAAABG7VuIVtV3V9WXq+q/V9W79utx4LSdpQcAOJ/fXHoA
gCezs/QAHCL7EqJVdUmSn0jyhiTfnOT7quqV+/FYcNrO0gMAnM/DSw8A8GR2lh6AQ2S/zohel+Sh
7n6kux9LcmeSG/fpsQAAADhA9itEr0jy6J7t317tAwAA4JC7dMkHr6olH/5A8ZVaz79YeoADxPcf
G7W99AAHyC8sPcDB4DmKzfNnaj1+mlqX56mnZ79C9ESSl+zZvnK17wnd7f8cAADAIbRfS3M/k+Tq
qrqqqp6T5M1J7t6nxwIAAOAA2Zczot39tar6h0nuzW7s/mR3P7AfjwUAAMDBUt299AwAAAAcIvu1
NBcAAADOSogCAMAhV1XPX3oGDpdF374Fnqqq+kiSc64r7+4bBscBOKequiLJVdnzd253/+JyEwH8
iap6XZL3J3lhkpdU1auSvK27b112Mi52QpSD6l+tfv1bSY4m+Q+r7e9LcmqRiQDOUFV3JPk7SY4n
+dpqdycRosAzxXuTvCGrd7jo7i9U1V9ddiQOAyHKgdTdv5AkVfWvu/u1ez70kar67EJjAZzppiSv
6O4/WnoQgHPp7kerau+ur53rWNgUrxHloHtBVf3F0xtV9bIkL1hwHoC9fiPJs5ceAuBJPLpanttV
9eyq+sdJvO0i+84ZUQ66f5Rkp6p+I0ll93VYb1t2JIAnfDXJ56vqE0meOCva3e9YbiSAb/CDSX48
yRVJTiS5N8nbF52IQ8H7iHLgVdVzk7xytfllS+CAZ4qqesvZ9nf3selZAOCZRIhyoK0uNf5DSa7q
7n9QVS/P7uuxPrrwaABJkqp6XpKXdPeDS88CcKaq+kDO8k4E3X3LAuNwiHiNKAfdB5L8cZLvXG2f
SPIjy40D8Ceq6nuTfD7Jx1bbr66qu5edCuAbfDTJz63++0SSb0rylUUn4lBwRpQDrao+292vrar7
u/s1q31f6O5XLT0bQFX9WpLvSrKz5znqv3X3tyw7GcDZVdUlSX6pu1+39Cxc3JwR5aD749Wyt06S
qvpL2XNBEICFPdbd//uMfV9fZBKA9bw8yeVLD8HFz1VzObBq9w2v/l12l7y9uKo+mOT1Sd665FwA
e3ypqr4/ybNWr2F/R5JfWXgmgCdU1f/J7j/o1+rXk0netehQHAqW5nKgVdUXk2wl+Y7sPoH+anf/
z0WHAlhZXVDtnyW5frXrniQ/0t3/b7mpAGB5QpQDraqOJfmJ7v7M0rMAnEtVPb+7v7r0HACnVdVf
frKPd/fnpmbhcBKiHGhV9eUkVyd5JMn/zWpZSXd/66KDASSpqtcleX+SF3b3S6rqVUne1t23Ljwa
cMhV1af2bO4NgtM/S33X8EgcMkKUA62qrjrb/u5+ZHoWgDNV1X1J/naSu101F3gmWl308dYkfyW7
Qfpfk/xbLyFgv7lYEQea4ASe6br70d1rqz3ha0vNAnAWx5L8QZJ/s9r+/iQ/leTmxSbiUBCiALB/
Hl0tz+2qenaSdyZ5YOGZAPb6lu6+ds/2p6rq+GLTcGh4H1EA2D8/mOTtSa5IciLJq1fbAM8Un6uq
7zi9UVXfnuSzC87DIeGMKADsg6p6VpK/290/sPQsAGdavQVeJ3l2kl+pqt9abV+V5MtLzsbh4GJF
ALBPquoz3f1tS88BcKZzXfDxNNfhYL8JUQDYJ1X13uyebfiP2X2LqSTenw8AhCgA7JM979N3+i9b
788HAPEaUQDYTx/NboSefv+WTvIHVfXq7v78cmMBwLKcEQWAfVJVH0ry2iR3ZzdGvyfJryd5aZKf
6e73LDcdACxHiALAPqmqX0zypu7+ymr7hUl+Lsl3J/m1M967DwAODe8jCgD75/Ikf7Rn+7EkR7r7
D8/YDwCHiteIAsD++WCS+6rqw6vt703yoap6QZLjy40FAMuyNBcA9lFVvTbJ61ebv9zdn11yHgB4
JhCiAAAAjPIaUQAAAEYJUQAAAEYJUQAAAEYJUQAAAEb9f4snvMLVya+DAAAAAElFTkSuQmCC
"
>
</div>

</div>

</div>
</div>

</div>
    </div>
  </div>
</body>
</html>
