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
\newcommand{\mb}[1]{\boldsymbol{#1}}
\newcommand{\mc}[1]{\mathcal{#1}}
\newcommand{\md}[1]{\mathbb{#1}}
\newcommand{\ms}[1]{\mathsf{#1}}
\newcommand{\mt}[1]{\mathtt{#1}}
\newcommand{\NN}{\md{N}}
\newcommand{\ZZ}{\md{Z}}
\newcommand{\QQ}{\md{Q}}
\newcommand{\RR}{\md{R}}
\newcommand{\CC}{\md{C}}
\newcommand{\KK}{\md{K}}

\newcommand{\Id}{\operatorname{Id}}
\newcommand{\sign}{\operatorname{sign}}
\newcommand{\abs}[1]{\left|#1\right|}
\newcommand{\norm}[1]{\left\|#1\right\|}
\newcommand{\inner}[2]{\left\langle#1, #2\right\rangle}
\newcommand{\diam}{\operatorname{diam}}
\newcommand{\floor}[1]{\left\lfloor#1 \right\rfloor}
\newcommand{\ceil}[1]{\left\lceil#1 \right\rceil}

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

\newcommand{\definition}[2]{
  @@definition
  **Definition** (_!#1_)
  #2
  @@
}

\newcommand{\proposition}[1]{
  @@proposition
  **Proposition**
  #1
  @@
}
\newcommand{\propositionT}[2]{
  @@proposition
  **Proposition** (_!#1_)
  #2
  @@
}

\newcommand{\proof}[1]{
  @@proof
  **Proof**
  #1 $\blacksquare$
  @@
}

\newcommand{\example}[1]{
  @@example
  **Example**
  #1
  @@
}
