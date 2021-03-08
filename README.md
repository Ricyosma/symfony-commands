# symfony
SYMNFONY cheatsheet

START:
composer create-project symfony/website-skeleton my-project

Next:
Change directory (cd (naam) )

DB:
Change database name. Put db on. then:
php bin/console doctrine:database:create

Overige commands:
php bin/console make:controller-> om een controller met bijbehorende view te bouwen.
php bin/console make:entity-> om een entiteit te definieren, blauwdruk van een tabel in je database.
php bin/console doctrine:schema:update --force-> de database schema instellingen wegschrijven in dbase afgeleid van de entiteiten.
php bin/console make:crud-> om de crud te bouwen.

Om webpack en npm hebben als je het nodig hebt:
 composer require symfony/webpack-encore-bundle
 yarn install

Voor user security bundle:
composer require symfony/security-bundle
php bin/console make:user
php bin/console make:auth

Bootstrap:
twig(staat in config):
    default_path: '%kernel.project_dir%/templates'
    form_themes:
        - 'bootstrap_4_horizontal_layout.html.twig'




Voor een naf bar (verander de juiste dingen)
<nav class="sticky-top navbar navbar-expand-lg navbar-light">
    <a class="navbar-brand" href="{{ path('home') }}">
        <img class="img-fluid" src="{{ asset('images/logo_innovatiehub.svg') }}" alt="BigData">
    </a>
    <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarSupportedContent"
            aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
        <span class="navbar-toggler-icon"></span>
    </button>
    <!-- TODO: add active class based on URL -->
    <div class="collapse navbar-collapse" id="navbarSupportedContent">
        <ul class="navbar-nav ml-auto mr-4">
            <li class="nav-item">
                <a class="nav-link active" href="{{ path('home') }}">Home <span class="sr-only">(current)</span></a>
            </li>
            <li class="nav-item disabled">
                <a class="nav-link" href="{{ path('nieuws_index') }}">Nieuws</a>
            </li>
            <li class="nav-item disabled">
                <a class="nav-link" href="{{ path('partner') }}">Partners</a>
            </li>
            <li class="nav-item disabled">
                <a class="nav-link" href="{{ path('contact') }}">Contact</a>
            </li>
        </ul>
</div>
</nav>
https://symfony.com/doc/current/doctrine/associations.html
https://symfony.com/doc/current/reference/forms/types/entity.html
https://github.com/dompdf/dompdf
https://ourcodeworld.com/articles/read/799/how-to-create-a-pdf-from-html-in-symfony-4-using-dompdf

        {% if app.user %}
            <a class="btn btn-secondary" href="{{ path('app_logout') }}">Logout</a>
        {% else %}
            <a class="btn btn-success mr-2" href="{{ path('app_login') }}">Login</a>
            <a class="btn btn-success" href="{{ path('app_register') }}">Register</a>
        {% endif %}

    public function __toString(): string{
        return $this->getEmail();

    }
