<!--
Global variables
-->
+++
author = "Alexandre Magueresse"
mintoclevel = 2
maxtoclevel = 4

# Add here files or directories that should be ignored by Franklin, otherwise
# these files might be copied and, if markdown, processed by Franklin which
# you might not want. Indicate directories by ending the name with a `/`.
# Base files such as LICENSE.md and README.md are ignored by default.
ignore = ["node_modules/"]

# RSS
generate_rss      = true
website_title     = "Alexandre Magueresse"
website_descr     = "Alexandre Magueresse"
website_url       = "https://alexandremagueresse.github.io/"
rss_full_content  = false
rss_author        = "alexandre.magueresse@gmail.com"
+++

<!--
Global latex commands
-->
\newcommand{\NN}{\mathbb{N}}
\newcommand{\ZZ}{\mathbb{Z}}
\newcommand{\QQ}{\mathbb{Q}}
\newcommand{\RR}{\mathbb{R}}
\newcommand{\CC}{\mathbb{C}}

\newcommand{\sign}{\operatorname{sign}}
\newcommand{\abs}[1]{\left|#1\right|}
\newcommand{\floor}[1]{\left\lfloor#1 \right\rfloor}

\newcommand{\eps}{\varepsilon}

\newcommand{\oo}[2]{\left(#1, #2\right)}
\newcommand{\oc}[2]{\left(#1, #2\right]}
\newcommand{\co}[2]{\left[#1, #2\right)}
\newcommand{\cc}[2]{\left[#1, #2\right]}

\newcommand{\backtonotes}{
    ~~~
    <div class="backtonote">
    ~~~
    $\blacktriangleleft$ [Back to notes](/notes)
    ~~~
    </div>
    ~~~
}