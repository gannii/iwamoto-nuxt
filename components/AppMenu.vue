<template>
	<div>

		<div id="g-menu-wrap">
	
			<div class="g-menu-head">

<!--
				<div class="cover">
					<span>
						<img src="@/assets/img/cover.jpg" alt="">
					</span>
				</div>
				<div class="avatar-lg">
					<nuxt-link to="/profile">
						<span>
							<img src="@/assets/img/avatar.jpg" alt="">
						</span>
					</nuxt-link>
				</div>
				<p>flower9292</p>

				<div class="logout">
					<a @click="logoutOAuth">
						<img src="@/assets/svg/icon_logout.svg" alt="ログアウト">
					</a>
				</div>
-->

				<div class="btn-signs">
					<ul>
						<li><a @click="loginOAuth">ログイン</a></li>
						<li><a class="fill" href="" target="_blank">新規登録</a></li>
						<li><a @click="logoutOAuth">ログアウト</a></li>
					</ul>
				</div>


			</div>

			<div class="g-menu-body">
				<nav id="g-menu">
					<ul>
						<li>
							<a href="#" target="_blank">
								<img src="@/assets/svg/icon_wallet.svg" alt="">
								<span>ウォレット</span>
							</a>
						</li>
<!--
						<li>
							<nuxt-link to="/">記事管理</nuxt-link>
						</li>
						<li>
							<nuxt-link to="/">全体お知らせ</nuxt-link>
						</li>
						<li>
							<nuxt-link to="/">個別お知らせ</nuxt-link>
						</li>
-->
						<li class="hasChild">
							<em>言語設定</em>
							<ul>
								<li>
									<a href="">日本語</a>
								</li>
								<li>
									<a href="">English</a>
								</li>
							</ul>
						</li>
					</ul>
				</nav>
			</div>

			<div class="g-menu-foot">
				<nuxt-link class="logo-rakun" to="/">
					<img src="@/assets/svg/logo_white.svg" alt="RAKUN">
				</nuxt-link>
				<aside>
					<ul>
						<li><nuxt-link to="/">利用規約</nuxt-link></li>
						<li><nuxt-link to="/">プライバシーポリシー</nuxt-link></li>
						<li><nuxt-link to="/company">運営会社</nuxt-link></li>
					</ul>
				</aside>
			</div>

		</div><!-- #g-menu-wrap -->

		<div id="btn-post">
			<nuxt-link to="/post">
				<img src="@/assets/svg/icon_pen.svg" alt="">
			</nuxt-link>
		</div>

		<div id="overlay"></div>

	</div>
</template>


<script>

import passport from 'passport'
// import OIDCStrategy from 'passport-azure-ad/lib/oidcstrategy.js'

// const OIDCStrategy = require('D:/_WORKS/017_rakun/gannii/rakunweb_front_bata/node_modules/passport-azure-ad/lib/oidcstrategy.js');

// const OIDCStrategy = require('passport-azure-ad')

export default {

/*
	middleware: [
		'auth',
	],
*/
	methods: {
		loginOAuth() {
			// this.$auth.loginWith('azul')

			passport.use(new OIDCStrategy({
			/*
			    identityMetadata: config.creds.identityMetadata,
			    clientID: config.creds.clientID,
			    responseType: config.creds.responseType,
			    responseMode: config.creds.responseMode,
			    redirectUrl: config.creds.redirectUrl,
			    allowHttpForRedirectUrl: config.creds.allowHttpForRedirectUrl,
			    clientSecret: config.creds.clientSecret,
			    validateIssuer: config.creds.validateIssuer,
			    isB2C: config.creds.isB2C,
			    issuer: config.creds.issuer,
			    passReqToCallback: config.creds.passReqToCallback,
			    scope: config.creds.scope,
			    loggingLevel: config.creds.loggingLevel,
			    loggingNoPII: config.creds.loggingNoPII,
			    nonceLifetime: config.creds.nonceLifetime,
			    nonceMaxAmount: config.creds.nonceMaxAmount,
			    useCookieInsteadOfSession: config.creds.useCookieInsteadOfSession,
			    cookieEncryptionKeys: config.creds.cookieEncryptionKeys,
			    clockSkew: config.creds.clockSkew,
			*/
				identityMetadata: 'https://login.microsoftonline.com/seqdiob2c.onmicrosoft.com/v2.0/.well-known/openid-configuration',
				clientID: '6346668f-ee75-42fe-bead-7bc650692334',
				responseType: 'id_token',
				responseMode: 'query',
				redirectUrl: 'http://localhost:3000',
				allowHttpForRedirectUrl: 'http://localhost:3000',
				isB2C: true,
				scope: 'openid https://seqdiob2c.onmicrosoft.com/laravel-api-mng/api_management'
			},
			function(iss, sub, profile, accessToken, refreshToken, done) {
			    if (!profile.oid) {
			    	return done(new Error("No oid found"), null);
			    }
			    // asynchronous verification, for effect...
			    process.nextTick(function () {
			      	findByOid(profile.oid, function(err, user) {
				        if (err) {
				        	return done(err);
				        }
				        if (!user) {
					        // "Auto-registration"
					        users.push(profile);
					        return done(null, profile);
				        }
				        return done(null, user);
				    	});
				    });
				}
			));
/*
			// app.get('/login', 
			this.$axios.$get('/login',
			passport.authenticate('azuread-openidconnect', { failureRedirect: '/' }),
			function(req, res) {
				log.info('Login was called in the Sample');
				res.redirect('/');
			});
*/

		},

		logoutOAuth() {
			// this.$auth.logout();

		}
	}
}
</script>